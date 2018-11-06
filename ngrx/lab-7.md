# NgRx Lab 7: Use NgRx Facades


### Scenario

NgRx **Facades** provide a public API layer between the NgRx layers and the View component layers. 

Architectures with Facades allow developers to implement views that maintain 1-way data flows and passively render *pushed data*.


### Code Instructions

Let's implement a TicketsFacade that encapsulates all the selectors to build Store Queries (e.g. `this.store.pipe(select(ticketsQuery.getAllTickets))`) and all store action dispatching.

  > Store queries are observables to specific NgRx state data; extracted with memoized selectors.

<br/>

----
  

##### In `libs/tickets-state/src/lib/+state/tickets.facade.ts`

1. Use the Angular Console (or CLI) to create a new service `TicketsFacade`.
2. Inject the Store using `private readonly store: Store<PartialAppState>`
3. Implement the following Query Observables using `store.pipe(select(<query>))`:
  * `allItems$`
  * `openItems$`: this observable will use the same filter that was formerly in the TicketList component.
  * `entities$`
  * `isLoading$`
  * `error$`  

Be sure to register the Facade as a service within the `tickets-state.module.ts`! And don't forget to add this service to the library barrel/Public API. 

> Be prepared to talked about why it should be in the barrel.

##### In `ticket-details.component.ts`

1. Replace the deprecated injection of Store within an injected Facade instance using `private facade: TicketsFacade`
2. Replace all uses of `store.pipe(select(<query>)` with `facade.entities$.pipe(...)`
3. Remove the dispatching of the `LoadTicket` action

##### In `ticket-list.component.ts`

1. Replace the deprecated injection of Store within an injected Facade instance using `private facade: TicketsFacade`
2. Replace all uses of `store.pipe(select(<query>)` with `facade.allItems$.pipe(...)`
3. Remove the dispatching of the `LoadTicket` action
4. Remove the deprecated filter function.

<br/>

### Code Snippets

###### `tickets.facade.ts`

![image](https://user-images.githubusercontent.com/210413/48090760-aa2d5900-e1bc-11e8-94c8-47fea4706b63.png)

###### `ticket-details.component.ts`
![image](https://user-images.githubusercontent.com/210413/47974960-709c0700-e071-11e8-97ad-e1d95e24b251.png)

###### `ticket-list.component.ts`
![image](https://user-images.githubusercontent.com/210413/48090776-b0233a00-e1bc-11e8-99ff-012eff0db287.png)

###### `tickets-state.module.ts`
![tickets-state.module.ts](https://user-images.githubusercontent.com/210413/47938212-574c5c80-deb1-11e8-9306-1159e67492ba.png)

<br/>

----

<br/>

### Investigate

In `ticket-details.component.ts`, why is the TicketDetails using the `entities$` query instead of the `allItems$`?

Be prepared to discuss this? 

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

Go to NgRx Lab #8: [Select Action and Loading Indicators](lab-8.md)
