# NgRx Lab 2: Effects and Redux Tools


### Scenario

Our Tickets view components use the HttpClient service to directly load ticket REST data. This is another poor design... views should never know how to load REST data.

Such async activity should be relegated to NgRx **Effects** classes!


<br/>

### Code Instructions

In this lab, you will:

  * Create an Effects class to handle async activity to load ticket REST data 
  * Update the view components to remove HttpClient usages; replaced with **LoadTicket** actions
  
<br/>

----
  
##### In `libs/tickets-state/src/lib/+state/tickets.effects.ts`

1. Implement a `@Effect loadAllTicket$` property that uses `this.actions.pipe()` for `TicketActionTypes.LOAD_ALL_TICKETS`, calls `ticketService.getTickets()` and then dispatches a LoadTicketsDone action.
1. Implement a `@Effect loadTicket$` property that uses `this.actions.pipe()` for `TicketActionTypes.LOAD_TICKET`, calls `ticketService.ticketById()` and then dispatches a LoadTicketDone action.

> Do not forget to register this Effects class in the `tickets-state.module.ts` **EffectsModule.forFeature()**
  
##### In `ticket-list.component.ts`

1. Remove the usage of `this.service.getTickets()`
2. Simply dispatch a `LoadTickets` action. 

##### In `ticket-details.component.ts`

1. Dispatch a `LoadTicket` action in the `ngOnInit()` 


<br/>

### Code Snippets

###### `tickets.effects.ts`

![tickets.effects.ts](https://user-images.githubusercontent.com/210413/47936640-4cdb9400-deac-11e8-94d5-46facc5d917b.png)

###### `tickets-list.component.ts`

![tickets-list.component.ts](https://user-images.githubusercontent.com/210413/47936662-5e24a080-deac-11e8-9aac-94536b13b02f.png)

###### `ticket-details.component.ts`

![ticket-details.component.ts](https://user-images.githubusercontent.com/210413/47936682-798fab80-deac-11e8-9543-443bd895157c.png)

<br/>


----

<br/>


### Investigate

Why are we dispatching a LoadTicket action in the TicketDetails component? What issue does this solve.


### Using Redux DevTools 

Open the Redux DevTools in Browser and watch the state changes and you route in the Customer-Portal application.

![image](https://user-images.githubusercontent.com/210413/47936825-f1f66c80-deac-11e8-8a17-d80f742bfdee.png)

> Install Chrome Extension: []Redux DevTools](https://chrome.google.com/webstore/detail/redux-devtools/lmhkpmbekcpmknklioeibfkpmmfibljd?hl=en)


<br/>

### Running the Application

*  Open the **Customer Portal** application with the browser: http://localhost:4203
*  Confirm the **Node Server** is running with browser page:  http://localhost:3000/api/tickets

Run the following command(s) in individual terminals:

```console
yarn server
```

```console
yarn customer-portal -- -o
```

> If you already have one(s) running and need to restart, you can stop the run with `ctrl+c`.


<br/>

----

<br/>


### Next Lab

Go to NgRx Lab #3: [Use Entity-like Pattern](lab-3.md)
