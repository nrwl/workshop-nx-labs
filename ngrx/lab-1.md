# NgRx Lab 1: Actions, Reducers, and Selectors

![image](https://user-images.githubusercontent.com/210413/47935906-02f1ae80-deaa-11e8-8cd7-0615e6234c76.png)

### Scenario

We have a **Customer Portal** application with **TicketList** and **TicketDetails** view components. Each component 
uses the HttpClient to load appropriate ticket data and store that data directly into the component. 

This is poor design since these components:
 
  * do not share the data... 
  * always reload the data [since routing creates new instances of the views]... 
  * contain business logic to load the data   

Let's use **NgRx** to store the data in a **Tickets* NgRx state layer. This lab (and the subsequent 6 other labs) will show developers how 
to use NgRx features and the beneficial impacts of NgRx on view components.

We already did some NgRx setup for you...

  * The Customer Portal application already has its `apps/customer-portal/src/app/app.module.ts` configured with NgRx
  * A **TicketsState** feature library `libs/tickets-state` with NgRx has also been created with initial actions, reducer, and selectors.

>  Take a moment to explore those files to quickly familiarize yourself with the NgRx artifacts and setup.


<br/>

### Code Instructions

In this lab, you will:

  * Use a LoadTicketsDone actions to store REST ticket data in the NgRx store 
  * Use a tickets reducer to process the LoadTicketsDone action
  * Use tickets selectors to build queries (into the NgRx state) for future ticket push-data 
  
<br/>

----
    
##### In `ticket-list.component.ts`

1. Inject the `store: Store<PartialAppState>` in the constructor
2. In constructor, use the HttpClient `ticketService.getTickets()` to load the tickets and then save the ticket data to the NgRx state by dispatching a `new LoadTicketsDone()` action. 
3. Prepare the `tickets$ : Observable<Ticket[]>` property using `this.store.pipe(select())` instead of the HttpClient service.

> Do not use imports that by-pass the library public api. E.g. `import { LoadTicketsDone } from '@tuskdesk-suite/tickets-state/src/...'`
  
##### In `ticket-details.component.ts`

1. Inject the `store: Store<PartialAppState>` in the constructor
2. In `ngOnInit()`, use `ticketsQuery.getAllTickets` with `store.pipe(select())` to get a list of all available tickets and then use the router param ticket `id` to extract the ticket.  
3. When the `service.ticketById(id)` returns the ticket, save that ticket to the NgRx state using `LoadTicketDone()`

##### In `tickets.reducer.ts`

1. Add `case TicketActionTypes.LOAD_ALL_TICKETS_DONE:` to process the **LoadTicketsDone** action and update the state.

<br/>


### Code Snippets

###### `ticket-list.component.ts`

![ticket-list.component.ts](https://user-images.githubusercontent.com/210413/47936257-16514980-deab-11e8-9878-dfbfe4eed6cb.png)

###### `ticket-details.component.ts`

![image](https://user-images.githubusercontent.com/210413/48030527-f6be5900-e116-11e8-96c8-572451b01ad9.png)


###### `tickets.reducer.ts`

![tickets.reducer.ts](https://user-images.githubusercontent.com/210413/47936309-44368e00-deab-11e8-8338-c92682a93420.png)



<br/>

----


<br/>

### Investigate

This improvement assumes that the NgRx **TicketsState** will contain the desired `ticket` for the ticket-details view. In what scenarios will this not work? Also, what would happen if you forgot to update the `tickets.reducer.ts` to process the `LoadTicketsDone` action?


Be prepared to discuss these issues and possible workarounds. 


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

Go to NgRx Lab #2: [Composed Store Selectors](lab-2.md)
