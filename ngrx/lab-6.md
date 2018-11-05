# NgRx Lab 6: Use DataPersistence fetch() & navigate()


### Scenario

Nx provides a **DataPersistence** feature to manage pessimistic and optimistic updates, data fetch, and Router navigation operations.

Data fetching implemented naively suffers from race conditions and poor error handling. `DataPersistence::fetch` addresses these problems; 
it runs all fetches in order, which removes race conditions and forces the developer to handle errors.


### Code Instructions

Let's create a Router effects class to auto-dispatch ticket Load actions when routing to ticket views.
Also, let's reduce the complexity in our `ticket.effects` implementation by using DataPersistence. 

Then we can remove deprecated *load* action code that is no longer needed in our views. 

<br/>

----
  
##### In `ticket.actions.ts`

1. Create a `RouterLoadTicket` action with a `ROUTER_LOAD_TICKET` enum. This action will have payload of `ticketId`.

##### In `libs/ticket-list-view/src/lib/+state/router.effects.ts`

1. Inject the `private d: DataPersistence<any>` into the constructor.
2. Implement `@Effect() loadview_TicketList$` which uses `this.d.navigation()` to auto-run a callback function when routing to a **TicketListComponent**. The callback function should dispatch a `LoadTickets` action.
  > This solution will auto-dispatch the 'load tickets' action when routing to the TicketList view... very nice! 
3. Implement `@Effect() loadview_TicketDetails$` which uses `this.d.navigation()` to auto-run a callback function when routing to a **TicketDetailsComponent**. The callback function should dispatch a `RouterLoadTicket` action.
  > This solution will auto-dispatch a special load ticket action when routing to the views... very nice! 

##### In `tickets.effects.ts`

1. Add a **Action Switcher**  new `@Effect() routeToTicket$` that listens to the NgRx `action$` stream for ROUTER_LOAD_TICKET and switches to emit a `LoadTicket` action.
2. Update `@Effect() loadTickets$` to use `this.d.fetch(...)` instead of `this.actions.pipe`. fetch() listens for `LOAD_ALL_TICKETS` and calls `run` callback should still use the HttpClient service and dispatch `LoadTicketsDone`.
3. Implement an `OnError` callback to dispatch `LoadTicketsError`
4. Update `@Effect() loadTicket$` to use `this.d.fetch(...)`instead of `this.actions.pipe`. fetch() listens for `LOAD_TICKET` and uses the `run` callback should still use the HttpClient service and dispatch `LoadTicketDone`.

> Notice how many of the operators (`mergeMap`, `exhaustMap`, and `catchError`) are no longer needed.

##### In `ticket-list.component.ts`

1. Delete the deprecated code `this.store.dispatch(new LoadTickets());`

##### In `ticket-details.component.ts`

1. Delete the deprecated code `this.store.dispatch(new LoadTicket());`


<br/>

### Code Snippets

###### `libs/ticket-list-view/src/lib/+state/router.effects.ts`

![router.effects.ts](https://user-images.githubusercontent.com/210413/47971894-d54c6700-e05b-11e8-944d-ff5db30b20c6.png)

  > Don't forget to register this `RouterEffects` with `EffectsModule.forRoot()` 


###### `tickets.effects.ts`

![ticket.effects.ts](https://user-images.githubusercontent.com/210413/47971891-c9f93b80-e05b-11e8-85bd-004f1f0dc6c6.png)

###### `ticket-list.component.ts`

![ticket-list.component.ts](https://user-images.githubusercontent.com/210413/47937884-42bb9480-deb0-11e8-87dd-45de0135288b.png)


<br/>


----

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


## Next Lab

Go to NgRx Lab #7: [Use NgRx Facade](lab-7.md)
