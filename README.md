# Lab Instructions for Nx Workshop

Here are the labs for the Git repos:  workshop-nx-starter

## Organizing Code in a Workspace 

For your local repository, checkout branch [`m2start`](https://github.com/nrwl/workshop-nx-starter/tree/m2start):

1. [Create an App and a Lib](organizing-code-in-a-workspace/lab-1.md)
1. [Create a Lazy Loaded UI Lib](organizing-code-in-a-workspace/lab-2.md)
1. [Public APIs for Libs](organizing-code-in-a-workspace/lab-3.md)
1. [Run the Build Command and NPM Scripts](organizing-code-in-a-workspace/lab-4.md)

## RxJS

For your local repository, checkout branch [`m3start`](https://github.com/nrwl/workshop-nx-starter/tree/m3start):

1. [Add Subscriptions to Ticket Search Form](rxjs/lab-1.md)
1. [Throttle Assigned to User Field and Transform](rxjs/lab-2.md)
1. [Use SwitchMap](rxjs/lab-3.md)
1. [Create a Ticket Timer Observable](rxjs/lab-4.md)
1. [Track Tickets to Work With a Multi-Cast Observable](rxjs/lab-5.md)

## Building Blocks of NgRx  

For your local repository, checkout branch [`m5start`](https://github.com/nrwl/workshop-nx-starter/tree/m5start):

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

>  If you already have one(s) running and you need to restart, you can stop the run with `ctrl+c`.

<br/>

*  Open the **Customer Portal** application with the browser: http://localhost:4203 
*  Confirm the **Node Server** is running with browser page:  http://localhost:3000/api/tickets
  >  ![screen shot 2018-05-21 at 7 14 38 am](https://user-images.githubusercontent.com/210413/40307086-ca016b0c-5cc6-11e8-9fb4-6d3a8ad3dc72.png)

<br/>

The REST server also provides a help listing (with links) when viewing **http://localhost:3000/**.

![screen shot 2018-05-20 at 8 54 39 pm](https://user-images.githubusercontent.com/210413/40286980-0dec895c-5c70-11e8-98e1-76555b23f6a2.png)

----

<br/>

#### Restarting the App Server

Sometimes a change to TypeScript interfaces or adding new `*.ts` files <u>will not get picked up</u> by the watch processes. In such cases, you may need to stop/restart these... if you feel your code is correct but you are getting an error.


<br/>

----
