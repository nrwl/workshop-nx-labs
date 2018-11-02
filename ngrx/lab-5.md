# NgRx Lab 5: Use DataPersistence fetch(( and navigate()


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
  

##### In `libs/ticket-list-view/src/lib/+state/router.effects.ts`

1. Inject the `private d: DataPersistence<any>` into the constructor.
2. Implement `@Effect() loadAllTickets$` which uses `this.d.navigation()` to auto-run a callback function when routing to a **TicketListComponent**. The callback function should dispatch a `LoadTickets` action.
3. Implement `@Effect() loadTicket$` which uses `this.d.navigation()` to auto-run a callback function when routing to a **TicketDetailsComponent**. The callback function should dispatch a `LoadTicket` action.

This solution with auto-dispatch load ticket actions when routing to views... very nice! 

> Don't forget to register this `RouterEffects` with `EffectsModule.forRoot()` 

##### In `tickets.effects.ts`

1. Update `@Effect() loadAllTickets$` to use `this.d.fetch(...)` instead of `this.actions.pipe`. The `run` callback should still use the HttpClient service and dispatch `LoadTicketsDone`.
2. Implement an `OnError` callback to dispatch `LoadTicketsError`
3. Update `@Effect() loadTicket$` to use `this.d.fetch(...)` instead of `this.actions.pipe`. The `run` callback should still use the HttpClient service and dispatch `LoadTicketDone`.

> Notice how many of the operators (`mergeMap`, `exhaustMap`, and `catchError`) are no longer needed.

##### In `ticket-list.component.ts`

1. Delete the deprecated code `this.store.dispatch(new LoadTickets());`


<br/>

### Code Snippets

###### `router.effects.ts`

![router.effects.ts](https://user-images.githubusercontent.com/210413/47937862-2e779780-deb0-11e8-9d28-14812f93a3cb.png)

###### `tickets.effects.ts`

![tickets.effects.ts](https://user-images.githubusercontent.com/210413/47937875-3a635980-deb0-11e8-94b1-bce679c0107a.png)

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

Go to NgRx Lab #6: [Use NgRx Facade](lab-6.md)
