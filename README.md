# Lab Instructions for Nx Workshop

## Organizing Code in a Workspace
1. [Create an App and a Lib](organizing-code-in-a-workspace/lab-1.md)
1. [Create a Lazy Loaded UI Lib](organizing-code-in-a-workspace/lab-2.md)
1. [Public APIs for Libs](organizing-code-in-a-workspace/lab-3.md)
1. [Run the Build Command and NPM Scripts](organizing-code-in-a-workspace/lab-4.md)

## RxJs
1. [Add Subscriptions to Ticket Search Form](rxjs/lab-1.md)
1. [Throttle Assigned to User Field and Transform](rxjs/lab-2.md)
1. [Use SwitchMap](rxjs/lab-3.md)
1. [Create a Ticket Timer Observable](rxjs/lab-4.md)
1. [Track Tickets to Work With a Multi-Cast Observable](rxjs/lab-5.md)

## Building Blocks of NgRx
1. [Create a Root State for Logs](building-blocks-of-ngrx/lab-1.md)
1. [Refactor Tickets State to Use Key/Value Object](building-blocks-of-ngrx/lab-2.md)
1. [Refactor Tickets State to use NgRx Entity](building-blocks-of-ngrx/lab-3.md)
1. [Create a Feature State for Ticket Comments](building-blocks-of-ngrx/lab-4.md)


----

<br/>

### Running the Application

Run the following command(s) in individual terminals:

```console
npm run server
npm run customer-portal
```


*  Open the **Customer Portal** application with the browser: http://localhost:4203 
*  Confirm the **Node Server** is running with browser page:  http://localhost:3000/api/tickets

If you already have one(s) running and you need to restart, you can stop the run with `ctrl+c`.

#### Restarting the App Server

Sometimes a change to TypeScript interfaces or adding new `*.ts` files <u>will not get picked up</u> by the watch processes. In such cases, you may need to stop/restart these... if you feel your code is correct but you are getting an error.


<br/>

----
