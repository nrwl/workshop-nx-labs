# NgRx Lab 4: Use Entity-like Pattern


### Scenario

Often NgRx solutions contain large collections of data items with subsequent CRUD code in the Reducers. Before using **@ngrx/entity** to solve those issues, let's manually create a entity-like solution... to explore simple concepts and benefits.

<br/>

### Code Instructions

In this lab, you will update the TicketsState to use entity-like patterns in the following NgRx artifacts:

  * `tickets.interfaces.ts`
  * `tickets.reducer.ts`
  * `tickets.selectors.ts`
  
We will also introduce the support of a **selected** ticket in our TicketsState. 

> Note that no view components will need to be updated. This is only an NgRx-layer change! 
 
<br/>

----
 
##### In `tickets.interfaces.ts`

1. Replace the `list` property with `entities` and `ids`. Define an interface for the `entities`
```ts
export interface TicketDictionary {
  [key: number]: Ticket;
}
```
2. Add a `selectedId: number` property.

  
##### In `tickets.reducer.ts`

1. Update the `initialState: TicketsState` to match the updated `TicketsState` interface.
2. Update the `ticketsReducer` function 
  1. Update `case TicketActionTypes.LOAD_ALL_TICKETS_DONE` to build the entities and ids values appropriately
    > Use `tickets.reduce(()={},{...state.entities})` to build a new **entities** TicketDictionary instance.  
  2. Update `case TicketActionTypes.LOAD_TICKET_DONE` to simply add the ticket to the **TicketDictionary**

##### In `tickets.selectors.ts`

1. Create a `getEntities` selector.
2. Create a `getIds` selector.
3. Update the `getAllTickets` and `getSelectedTicket` selectors to use the new getEntities and getIds selectors.
4. export all the selectors as part of a namespace using `export namespace ticketsQuery { ... } `

<br/>


### Code Snippets

###### `tickets.interfaces.ts`

![tickets.interfaces.ts](https://user-images.githubusercontent.com/210413/47937224-0d15ac00-deae-11e8-9a3f-010c6a5e688b.png)

###### `tickets.reducer.ts`

![tickets.reducer.ts](https://user-images.githubusercontent.com/210413/47937238-169f1400-deae-11e8-84f0-963e54f0657b.png)

###### `tickets.selectors.ts`

![tickets.selectors.ts](https://user-images.githubusercontent.com/210413/47937253-1dc62200-deae-11e8-9ccd-5107b7e0ed42.png)


<br/>


----

<br/>

### Investigate

The selectors and reducer have become slightly more complex... but this initial complexity is only an aspect of an manual simulation of @ngrx/entity.

Consider these questions:

* Why did we use a `namespace ticketsQuery`? 
* Why did we add selected ticket features like `selectedId` and `getSelectedTicket`?

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


### Next Lab

Go to NgRx Lab #5: [Use @ngrx/entity](lab-5.md)
