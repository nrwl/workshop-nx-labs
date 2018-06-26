# Lab: Create a Root State for Logs

## Time: 30 minutes

## Scenario
We want to implement NgRx to handle the data for the list of event logs in the logs app. To do that we can create an app specific state lib and then create the root state boilerplate using the Nx schematics to scaffold out that code.

Make use of the Nx schematic for ngrx to generate the state files and modify those to store and load event logs, then use the store in the logs list component to display the logs. Configure the logs app to use the new logs state module.

---

## Instructions

1. Create a new lib named **logs-state** using the `lib` schematic.

  ```console
  ng g lib logs-state
  ```

2. Use the `ngrx` schematic to create a new **logsRoot** state. Target the **logs-state** lib by using the `--module` option and path to the module file in logs-state. Use the `--root` flag to make it a root state.

  ```console
  ng g ngrx logs-root --root --module=./libs/logs-state/src/lib/logs-state.module.ts
  ```

## Important Note!

At this point, there is an invalid import path inside `logs-state.module.ts`: `../environments/environment`. Ignore this for now, we'll move this in step 8.

3. Add an `eventLogs` property to the `LogsRootData` interface and set it as the type of an array of `EventLog` objects. Update the logs root init object to have an `eventLogs` property set to an empty array.

  ###### file: libs/logs-state/src/lib/+state/logs-root.reducer.ts

  ```ts
  export interface LogsRootData  { eventLogs: EventLog[];  }          // managed data within this Feature
  export interface LogsRootState { readonly logsRoot: LogsRootData; } // slice of Store state (aka Feature)

  export const initialState: LogsRootData = { eventLogs: []   };      // initial managed state
  ```

4. Update the loaded action payload in `LogsRootLoaded` to be an array of `EventLog` objects.

  ###### file: libs/logs-state/src/lib/+state/logs-root.action.ts

  ```ts
  export class LogsRootLoaded implements Action {
    readonly type = LogsRootActionTypes.LogsRootLoaded;
    constructor(public payload: EventLog[]) {}
  }
  ```

5. Change the logs root reducer to use the updated type name and use the payload to set the eventLogs state.


###### file: libs/logs-state/src/lib/+state/logs-root.reducer.ts

```ts
    case LogsRootActionTypes.LogsRootLoaded: {
      return { ...state, eventLogs : action.payload };
    }
```


6. Refactor the logs root effects constructor to inject the `LogService`, use `ofType` and `mergeMap` to load the logs.

###### file: libs/logs-state/src/lib/+state/logs-root.effects.ts

```typescript
  @Effect()
  loadLogsRoot$ = this.actions$.ofType(LogsRootActionTypes.LoadLogsRoot).pipe(
    mergeMap(action => {
      return this.logsService
        .logs()
        .pipe(
          map(logs => new LogsRootLoaded(logs)),
          catchError(_ => of(null))
        );
    })
  );
```

> Note: For now, be sure to disable the existing `@Effect() effect$` code...

<br/>

7. Update the public api for the **logs-state** so you can expose the pieces needed in the `forRoot` registrations (like the reducer and initial state, etc).

###### file: libs/logs-state/src/index.ts

```ts
export { LogsStateModule } from "./lib/logs-state.module";
export { LogsRootEffects } from "./lib/+state/logs-root.effects";
export { LoadLogsRoot, LogsRootLoaded } from "./lib/+state/logs-root.actions";
export { initialState as logsRootInitialState, logsRootReducer, LogsRootState } from "./lib/+state/logs-root.reducer";
```

  >  Also export the `LogsRootState` to make it public so it can be used in the **logs-view** lib.

<br/>

8. Move the `StoreModule.forRoot` and `EffectsModule.forRoot` out of the lib module and into the logs app module (the forRoot calls should be provisioned in the app at the root module). Also move the `!environment.production ? StoreDevtoolsModule.instrument() : []` import out of the `LogStateModule` and up to the **logs** app module so it has access to the `environment` object.

###### file: libs/logs-state/src/logs-state.module.ts

```ts
import { NgModule } from "@angular/core";
import { CommonModule } from "@angular/common";
import { LogsRootEffects } from "./+state/logs-root.effects";

@NgModule({
  imports: [CommonModule],
  providers: [LogsRootEffects]
})
export class LogsStateModule {}

```

###### file: apps/logs/src/app/app.module.ts

```ts
import { LogsBackendModule } from '@tuskdesk-suite/logs-backend';
import { logsRootInitialState, logsRootReducer, LogsRootEffects } from '@tuskdesk-suite/logs-state';

@NgModule({
  imports: [
    BrowserModule,
    NxModule.forRoot(),
    StoreModule.forRoot(
      { logsRoot: logsRootReducer },
      {
        initialState: {
          logsRoot: logsRootInitialState
        },
        metaReducers: !environment.production ? [storeFreeze] : []
      }
    ),
    EffectsModule.forRoot([LogsRootEffects]),
    !environment.production ? StoreDevtoolsModule.instrument() : [],
    RouterModule.forRoot([
        { path: '', loadChildren: '@tuskdesk-suite/logs-view#LogsViewModule' }
      ],
      { initialNavigation: 'enabled' }
    ),
    LogsBackendModule
  ],
  declarations: [AppComponent],
  bootstrap: [AppComponent]
})
export class AppModule {}

```

  >  Remember: `.forRoot()`, `environment` and root providers all belong in the app shells, not in the lib modules.

<br/>

9. Add the `LogsRootQuery` query registry to the `logs-root.reducer.ts`
```ts
export const LogsRootQuery = {
  getEventLogs : (s) => s.logsRoot.eventLogs
}
```

> Don't forget to export this in the barrel file (aka Public API)

10. Refactor the logs list component in the **logs-view** lib to dispatch the action to load logs. Don't forget to select the event logs from the store.

###### file: libs/logs-view/src/lib/logs-list/logs-list.component.ts

```ts
export class LogsListComponent {
  logs$: Observable<EventLog[]> = this.store.select(LogsRootQuery.getEventLogs);

  constructor(private store: Store<LogsRootState>) {
    this.store.dispatch(new LoadLogsRoot({});
  }
}

```

<br/>

## Viewing in the Browser
Run the following command(s) in individual terminals:
- `npm run server`
- `npm run logs`

Open up the browser to:
- http://localhost:4204 (logs app)

If you already have one(s) running and you need to restart, you can stop the run with `ctrl+c`.

*(Note: sometimes a change to TypeScript interfaces will not get picked up by the watch so you may need to stop/restart these if you feel your code is correct but you are getting an error)*

If you have the Redux DevTools extension installed, open that up either under the dev tools panel or via the icon in the top browser bar. Usually you will have to have this open before hitting the site for the data to load, so if you don't see data try refreshing the page.

## Next Lab
Go to Building Blocks of NgRx Lab #2: [Refactor Tickets State to Use Key/Value Object](lab-2.md)
