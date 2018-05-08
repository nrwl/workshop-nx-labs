# Lab: Public APIs for Libs

### Scenario
> Time: 15 minutes

Just because we put code in a lib doesn't mean that we intend for it to be used outside of that lib. Some lib code should be made public and some should remain internal to the lib. The `index.ts` files in the libs provide a place to export code that is intended to be public.

The time has come to replace the temporary logs data with actual data from the backend API. 
*  Create a new model interface for event logs, and 
*  Use the Angular CLI to generate a new service to fetch the logs with the Angular **HttpClient**. 
*  Use the `index.ts` files to export the bits that need to be used outside of the libs.

## Instructions

1. Create a new interface for an `EventLog` data model in the **data-models** lib.

###### libs/data-models/src/data-models.ts

```js
export interface EventLog {
  id: number;
  message: string;
  userId: number;
  resourceType: string;
  resourceId: number;
}
```

2. Export the `EventLog` in the **data-models** `index.ts` file to make it "public".

1. Add the `HttpClientModule` to the **logs-backend** module.

6. The `ApiConfig` type is not public (you should see the tslint error). Make it **public** by adding an export of it to the **backend** lib `index.ts` file. Back in the `LogService` make sure the import path for `ApiConfig` is set to `@tuskdesk-suite/backend`.

   >  Do not use `import { ApiConfig } from '../../backend/src/api-config';`
   

1. Use the Angular CLI schematic for generating a new service to create a new service named **log** to the **logs-backend** lib with the `-a` option. Include the `module` option to tell the CLI schematic to include the service in the `providers` NgModule metadata (`--module=logs-backend.module.ts`).

   >  `ng g service log -a=<lib-name> --module=logs-backend.module.ts`

1. Set up the `LogService` logic:

###### libs/logs-backend/src/log.service.ts

```typescript
export class LogService {
  private _rootUrl = '';
  constructor(@Optional() private apiConfig: ApiConfig, private http: HttpClient) {
    if (apiConfig) {
      this._rootUrl = apiConfig.rootUrl;
    }
  }
  logs(): Observable<EventLog[]> {
    return this.http.get<EventLog[]>(`${this._rootUrl}/api/eventlogs`);
  }
}
```

   >  Make sure you add the necessary import statements!

   
7. Add an export for the `LogService` to the **logs-backend** `index.ts` file to make it public.

8. Refactor the `LogsListComponent` to inject the `LogService` (use the npm scope short path for the import) and use it to get logs from the `logs` method. You can `subscribe` to that and set the `logs` class field with the data, or you can make use of the `async` pipe.

###### libs/logs-view/src/logs-list/logs-list.component.ts

```ts
import { LogService } from '@tuskdesk-suite/logs-backend';

@Component({
  selector: 'app-logs-list',
  templateUrl: './logs-list.component.html',
  styleUrls: ['./logs-list.component.scss']
})
export class LogsListComponent implements OnInit {
  logs : EventLog[];  // or use observable...

  constructor(private logService: LogService) {}

  ngOnInit() {

  }
}  
  ```


---

### Viewing in the Browser

<br/>

<img width="1440" alt="screen shot 2018-04-17 at 12 00 27 am" src="https://user-images.githubusercontent.com/210413/38851293-6dd66dbe-41d2-11e8-8d02-324226819ce7.png">


Run the following command(s) in individual terminals:
- `npm run server`
- `npm run logs`

Open up the browser to:
- http://localhost:4204 (logs app)

If you already have one(s) running and you need to restart, you can stop the run with `ctrl+c`.

*(Note: sometimes a change to TypeScript interfaces will not get picked up by the watch so you may need to stop/restart these if you feel your code is correct but you are getting an error)*

## Next Lab
Go to Organizing Code in a Workspace Lab #4: [Run the Build Command and NPM Scripts](lab-4.md)
