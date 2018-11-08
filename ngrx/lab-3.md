# NgRx Lab 3: Effects and Redux Tools


### Scenario

Our Tickets view components use the HttpClient service to directly load ticket REST data. This is another poor design... views should never know how to load REST data.

Such async activity should be relegated to NgRx **Effects** classes!

![image](https://user-images.githubusercontent.com/210413/47959514-0d986a80-dfb4-11e8-9a6f-a52c53cbbdcd.png)

<br/>

### Code Instructions

In this lab, you will:

  * Create an Effects class to handle async activity to load ticket REST data 
  * Update the view components to remove HttpClient usages; replaced with **LoadTicket** actions
  
<br/>

----
  
##### In `libs/tickets-state/src/lib/+state/tickets.effects.ts`

1. Implement a `@Effect loadAllTicket$` property that uses `this.actions.pipe()` for `TicketActionTypes.LOAD_ALL_TICKETS`, calls `ticketService.getTickets()` and then dispatches a LoadTicketsDone action.
2. Implement a `@Effect loadTicket$` property that uses `this.actions.pipe()` for `TicketActionTypes.LOAD_TICKET`, calls `ticketService.ticketById()` and then dispatches a LoadTicketDone action.

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

<a href="https://carbon.now.sh/?bg=rgba(255%2C255%2C255%2C1)&t=seti&wt=none&l=application%2Ftypescript&ds=false&dsyoff=6px&dsblur=8px&wc=true&wa=true&pv=48px&ph=32px&ln=false&fm=Hack&fs=14px&lh=133%25&si=false&code=%252F%252F%2520tickets.effects.ts%250A%250Aimport%2520%257B%2520Injectable%2520%257D%2520from%2520%27%2540angular%252Fcore%27%253B%250Aimport%2520%257B%2520Effect%252C%2520Actions%252C%2520ofType%2520%257D%2520from%2520%27%2540ngrx%252Feffects%27%253B%250A%250Aimport%2520%257B%2520catchError%252C%2520exhaustMap%252C%2520map%252C%2520mergeMap%2520%257D%2520from%2520%27rxjs%252Foperators%27%253B%250Aimport%2520%257B%2520TicketService%2520%257D%2520from%2520%27%2540tuskdesk-suite%252Fbackend%27%253B%250A%250Aimport%2520%257B%250A%2520%2520LoadTicket%252C%250A%2520%2520LoadTickets%252C%250A%2520%2520TicketActionTypes%252C%250A%2520%2520LoadTicketsDone%252C%250A%2520%2520LoadTicketDone%252C%250A%2520%2520LoadTicketsError%252C%250A%2520%2520LoadTicketError%250A%257D%2520from%2520%27.%252Ftickets.actions%27%253B%250Aimport%2520%257B%2520of%2520%257D%2520from%2520%27rxjs%27%253B%250A%250A%2540Injectable()%250Aexport%2520class%2520TicketsEffects%2520%257B%250A%2520%2520%252F**%250A%2520%2520%2520*%2520Load%2520All%2520Tickets%2520and%2520update%2520state%2520upon%2520server%2520response%250A%2520%2520%2520*%252F%250A%2520%2520%2540Effect()%250A%2520%2520loadTickets%2524%2520%253D%2520this.actions.pipe(%250A%2520%2520%2520%2520ofType%253CLoadTickets%253E(TicketActionTypes.LOAD_ALL_TICKETS)%252C%250A%2520%2520%2520%2520exhaustMap(()%2520%253D%253E%2520%257B%250A%2520%2520%2520%2520%2520%2520return%2520this.ticketService.getTickets().pipe(%250A%2520%2520%2520%2520%2520%2520%2520%2520map(tickets%2520%253D%253E%2520new%2520LoadTicketsDone(tickets))%252C%250A%2520%2520%2520%2520%2520%2520%2520%2520catchError(err%2520%253D%253E%2520%257B%250A%2520%2520%2520%2520%2520%2520%2520%2520%2520%2520return%2520of(new%2520LoadTicketsError(err.toString()))%253B%250A%2520%2520%2520%2520%2520%2520%2520%2520%257D)%250A%2520%2520%2520%2520%2520%2520)%253B%250A%2520%2520%2520%2520%257D)%250A%2520%2520)%253B%250A%250A%2520%2520%252F**%250A%2520%2520%2520*%2520Load%2520Ticket%2520by%2520Id%2520and%2520update%2520state%2520upon%2520server%2520response%250A%2520%2520%2520*%252F%250A%2520%2520%2540Effect()%250A%2520%2520loadTicketById%2524%2520%253D%2520this.actions.pipe(%250A%2520%2520%2520%2520ofType%253CLoadTicket%253E(TicketActionTypes.LOAD_TICKET)%252C%250A%2520%2520%2520%2520map(action%2520%253D%253E%2520action.ticketId)%252C%250A%2520%2520%2520%2520mergeMap(ticketId%2520%253D%253E%2520%257B%250A%2520%2520%2520%2520%2520%2520return%2520this.ticketService.ticketById(ticketId).pipe(%250A%2520%2520%2520%2520%2520%2520%2520%2520map(ticket%2520%253D%253E%2520new%2520LoadTicketDone(ticket))%252C%250A%2520%2520%2520%2520%2520%2520%2520%2520catchError(err%2520%253D%253E%2520%257B%250A%2520%2520%2520%2520%2520%2520%2520%2520%2520%2520return%2520of(new%2520LoadTicketError(err.toString()))%253B%250A%2520%2520%2520%2520%2520%2520%2520%2520%257D)%250A%2520%2520%2520%2520%2520%2520)%253B%250A%2520%2520%2520%2520%257D)%250A%2520%2520)%253B%250A%250A%2520%2520constructor(private%2520actions%253A%2520Actions%252C%2520private%2520ticketService%253A%2520TicketService)%2520%257B%257D%250A%257D%250A&es=2x&wm=false&ts=false" target="_blank">
![tickets-list.component.ts](https://user-images.githubusercontent.com/210413/47936662-5e24a080-deac-11e8-9aac-94536b13b02f.png)
</a>

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

Go to NgRx Lab #4: [Use Entity-like Pattern](lab-4.md)
