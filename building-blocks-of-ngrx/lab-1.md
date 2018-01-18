# Lab: Create a Root State for Logs

## Scenario
We want to implement NgRx to handle the data for the list of event logs in the logs app. To do that we can create an app specific state lib and then create the root state boilerplate using the Nx schematics to scaffold out that code.

Make use of the Nx schematic for ngrx to generate the state files and modify those to store and load event logs, then use the store in the logs list component to display the logs. Configure the logs app to use the new logs state module.

## Instructions
1. Create a new lib named **logs-state** using the `lib` schematic.
1. Use the `ngrx` schematic to create a new **logsRoot** state. Target the **logs-state** lib by using the `--module` option and path to the module file in logs-state. Use the `--root` flag to make it a root state.
1. Add an `eventLogs` property to the `LogsRoot` interface and set it as the type of an array of `EventLog` objects.
1. Update the logs root init object to have an `eventLogs` property set to an empty array.
1. Change the logs root actions to have unique names for the actions and update the loaded action payload to be an array of `EventLog` objects.
1. Change the logs root reducer to use the updated type name and use the payload to set the eventLogs state.
1. Refactor the logs root effects to constructor inject the `LogService`, use `ofType` and `mergeMap` to load the logs.
```
@Effect()
loadData = this.actions.ofType('LOAD_DATA').pipe(
  mergeMap(action =>
    this.logService.logs().pipe(
      map(logs => {
        return {
          type: 'DATA_LOADED',
          payload: logs
        };
      }),
      catchError(() => of(null))
    )
  )
);
```
8. Import the `LogsStateModule` into the **logs** app module.
1. Move the `!environment.production ? StoreDevtoolsModule.instrument() : []` import out of the `LogStateModule` and up to the **logs** app module so it has access to the `environment` object.
1. Export the `LogsRootState` from the index.ts file in the **logs-state** lib to make it public.
1. Refactor the logs list component to dispatch the action to load logs and select the event logs from the store.

## Next Lab
Go to [Refactor Tickets State to Use Key/Value Object](lab-2.md)