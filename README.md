# Lab Instructions for Nx Workshop

![image](https://user-images.githubusercontent.com/210413/47935906-02f1ae80-deaa-11e8-8cd7-0615e6234c76.png)

Here are the labs synced with the git repos:  [workshop-nx-finisher](https://github.com/nrwl/workshop-nx-project)
  > When starting the workshop, developers will checkout [workshop-nx-starter](https://github.com/nrwl/workshop-nx-starter)

## Workspaces

For your local repository, checkout branch [`m2start`](https://github.com/nrwl/workshop-nx-starter/tree/m2start):

1. [Lab 1: Create an App and a Lib](organizing-code-in-a-workspace/lab-1.md)
1. [Lab 2: Create a Lazy Loaded UI Lib](organizing-code-in-a-workspace/lab-2.md)
1. [Lab 3: Public APIs for Libs](organizing-code-in-a-workspace/lab-3.md)
1. [Lab 4: Run the Build Command and NPM Scripts](organizing-code-in-a-workspace/lab-4.md)

## RxJS

For your local repository, checkout branch [`m3start`](https://github.com/nrwl/workshop-nx-starter/tree/m3start):

1. [Lab 1: Ticket Search DropDown](rxjs/lab-1.md)
1. [Lab 2: Throttle Search Requests](rxjs/lab-2.md)
1. [Lab 3: Use SwitchMap](rxjs/lab-3.md)
1. [Lab 4: Create a custom Observable](rxjs/lab-4.md)
1. [Lab 5: Use BehaviorSubject](rxjs/lab-5.md)

## NgRx  

For your local dev repository, checkout branch [`m5start`](https://github.com/nrwl/workshop-nx-starter/tree/m5start):

1. [Lab 1: Actions, Reducers, and Selectors](ngrx/lab-1.md)
1. [Lab 2: Composed Store Selectors](ngrx/lab-2.md)
1. [Lab 3: Effects and Redux Tools](ngrx/lab-3.md)
1. [Lab 4: Use Entity-like Pattern](ngrx/lab-4.md)
1. [Lab 5: Use @ngrx/entity](ngrx/lab-5.md)
1. [Lab 6: Use DataPersistence fetch() & navigate()](ngrx/lab-6.md)
1. [Lab 7: Use NgRx Facade](ngrx/lab-7.md)
1. [Lab 8: 8: Spinners, Select, & Action Deciders](ngrx/lab-8.md)

----

<br/>

## Running the Application

Run the following command(s) in individual terminals:

```console
npm run server
npm run customer-portal
```

>  If you already have one(s) running and you need to restart, you can stop the run with `ctrl+c`.

*  Open the **Customer Portal** application with the browser: http://localhost:4203 

----

<br/>

## Using the HTTP REST Server

Confirm the **Node Server** is running with browser page:  http://localhost:3000/api/tickets. Use terminal command to launch the server if needed: `npm run server`.

> You can easily throttle the server responses with random delays using `npm run server -- -throttled`

<br/>

![screen shot 2018-05-21 at 7 14 38 am](https://user-images.githubusercontent.com/210413/40307086-ca016b0c-5cc6-11e8-9fb4-6d3a8ad3dc72.png)

To see the server HELP page (with links), navigate to **http://localhost:3000/**.

![screen shot 2018-05-20 at 8 54 39 pm](https://user-images.githubusercontent.com/210413/40286980-0dec895c-5c70-11e8-98e1-76555b23f6a2.png)

#### Restarting the App Server

Sometimes a change to TypeScript interfaces or adding new `*.ts` files <u>will not get picked up</u> by the watch processes. In such cases, you may need to stop/restart these... if you feel your code is correct but you are getting an error.

If you already have one(s) running and you need to restart, you can stop the run with `ctrl+c`.

