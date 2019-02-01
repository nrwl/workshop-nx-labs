# NgRx Lab 5: Use @ngrx/entity


### Scenario

NgRx entity is designed to take care of data management in your state in a way that is efficient and performant. 

**@ngrx/entity** handles the store structure part and provides an easy way avoid tedious CRUD logic in your reducers.


### Code Instructions

Let's refactor the tickets state to use Entity instead of the hand crafted version you wrote last lab. Update the interface, initial state and reducer.
 
Then we will introduce selector functions as they are needed to get to the entities in the state. 

  > Take note how some of this will be easier to work with (and provide some additional mutation safety), but for other parts it will add some complexity.

<br/>

----
  

##### In `tickets.interfaces.ts`

1. Delete the `TicketDictionary` interface
2. Use `export interface TicketsState extends EntityState<Ticket> { ... }`

##### In `tickets.reducer.ts`

1. Implement an entity adapter `ticketsAdapter = createEntityAdapter<Ticket>()`
2. Implement an initialState builder function 
```ts
getInitialState = () => ticketsAdapter.getInitialState( <custom initializations> );`
```
3. In the ticketsReducer, use `...ticketsAdapter.addAll(tickets, state)` for **LoadTicketsDone** actions
4. In the ticketsReducer, use `...ticketsAdapter.upsertOne(ticket, state)` for **LoadTicketDone** actions 

##### In `tickets.selectors.ts`

1. Access the @ngrx/entity selectors using:
```typescript
const { selectAll, selectEntities } = ticketsAdapter.getSelectors();
```
2. Implement a `getTicketAsEntities` selector.
3. Update the `getAllTickets` and `getSelectedTicket` selectors to compose/use the @ngrx/entity selectors.


##### In `tickets-state.module.ts`

1. Use the initialState builder function in the feature store registration:
```typescript
 StoreModule.forFeature(FEATURE_TICKETS, ticketsReducer, { initialState: getInitialState }),
```

##### In `ticket-details.component.ts`

1. Use `select(ticketsQuery.getTicketAsEntities)` and lookup the ticket directly from the emitted dictionary. 



<br/>

### Code Snippets

###### `tickets.interfaces.ts`

![tickets.interfaces.ts](https://user-images.githubusercontent.com/210413/47937603-44d12380-deaf-11e8-818f-dc39ec631769.png)

###### `tickets.reducer.ts`

![tickets.reducer.ts](https://user-images.githubusercontent.com/210413/47937627-54506c80-deaf-11e8-90b2-4ceedb3af59f.png)

###### `tickets.selectors.ts`

![image](https://user-images.githubusercontent.com/210413/48032580-d0e88280-e11d-11e8-8dca-e58377cbb2ac.png)


###### `ticket-details.component.ts`

![image](https://user-images.githubusercontent.com/210413/48032726-62f08b00-e11e-11e8-9a5c-e28340300da7.png)



<br/>


----

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

Go to NgRx Lab #6: [Use DataPersistence `fetch()` and `navigate()`](lab-6.md)
