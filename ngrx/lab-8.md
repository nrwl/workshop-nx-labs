# NgRx Lab 8: Spinners, Select, & Action Deciders

### Scenario

Each time the user routes to the TicketDetails view, a LoadTicket action requests a refresh from the server. 
Let's instead *select* the ticket in the TicketList view and then query for the **selectedTicket** when we route to the TicketDetails view. 
And if the ticket is not available in our NgRx state, we will auto-load it.

> Note this solution will use an NgRx **Action Decider** to conditionally load ticket details remotely.

Also, let's simulate a delayed server responses and show a loading/in-progress UI indicator while we are loading REST ticket data.
 
### Extra Instructions

To properly see the spinning, loading indicators, you will need to simulate a slow network. The NodeJS server has a special `--throttle` argument that can be used to introduce random delays to the server's REST responses:


Run the following command(s) in individual terminals:

```console
yarn server --throttle
```

```console
yarn customer-portal -- -o
```

<br/>

----
  

#### Feature (a): **Loading Indicators**

<br/>

##### In `tickets-list-view.module.ts`

1. Import and register the `UiMaterialModule` so the TicketList and TicketDetails views can use the `mat-spinner` component.
 

##### In `tickets.reducer.ts`

1. Update `getInitialState()` to initialize with `loading: true`
2. Add `case TicketActionTypes.LOAD_TICKET: {...}` to update the state with `loading: true`
3. Update `case TicketActionTypes.LOAD_ALL_TICKETS_DONE:` to set `loading: false`
4. Update `case TicketActionTypes.LOAD_TICKET_DONE:` to set `loading: false`
 
 
##### In `ticket-list.component.ts`

1. Add a property `loading$ = this.facade.isLoading$;`
2. Update the template to hide the list content and show the spinner when the loading == true; use:
```html
<div *ngIf="!(loading$ | async) else loading" >
...
</div>
<ng-template #loading>
  <mat-spinner class="nrwl"></mat-spinner>
</ng-template>
```

##### In `ticket-details.component.ts`

1. Add a property `loading$ = this.facade.isLoading$;`
2. Update the template to hide the list content and show the spinner when the loading == true; use:


<br/>

##### **Code Snippets**

###### `tickets.reducer.ts`
![image](https://user-images.githubusercontent.com/210413/47971266-7ab00c80-e055-11e8-8d1d-e2b546c3abc3.png)


###### `ticket-list.component.html`
![ticket-list.component.html](https://user-images.githubusercontent.com/210413/47938584-97f8a580-deb2-11e8-9727-6db09c34e4f1.png)

###### `ticket-details.component.html`
![ticket-details.component.html](https://user-images.githubusercontent.com/210413/47938591-9e871d00-deb2-11e8-95bc-766713786cb4.png)


<br/>

----
  
<br/>

#### Feature (b): **SelectTicket**

<br/>

1. In `tickets.actions.ts`, add a `SelectTicket` enum and action class to `tickets.actions.ts` 
2. In `tickets.reducer.ts`, add a `case TicketActionTypes.SELECT_TICKET: {...}` to update the `selectedId` state value.

##### In `tickets.effects.ts`

Here we do not want to relaod the ticket if it is already loaded in our state cache. So we need to check if the ticket exists in our state and decide if we are selecting-only, or selecting AND loading the ticket details.

1. Make sure the `@Effect() loadTicket$` is listening for the `LoadTicket` action.
2. Create an `ticketRegistry$` Observable to our state Ticket entities using `select(ticketsQuery.getTicketAsEntities));`
2. Create a `@Effect() routeAndLoadTicket$` that listens on the NgRx `action$` stream for the ROUTER_LOAD_TICKET with a `run` callback that conditionally emits a `LoadTicket()` action. 
  > Use `withLatestFrom(ticketRegistry$)` to get all currently loaded tickets and check it the selected ticket has already been loaded. 


##### In `ticket-details.component.ts`

1. Use the TicketFacade `selectedTicket$` query to update the `ticket$ = this.facade.selectedTicket$`


<br/>

##### **Code Snippets**

###### `tickets.actions.ts`
![tickets.actions.ts](https://user-images.githubusercontent.com/210413/47938930-9380bc80-deb3-11e8-9ee2-78664af6edef.png)

###### `tickets.reducer.ts`
![tickets.reducer.ts](https://user-images.githubusercontent.com/210413/47938937-99769d80-deb3-11e8-957d-268d1b4482bb.png)

###### `tickets.facade.ts`
![tickets.facade.ts](https://user-images.githubusercontent.com/210413/47938946-a09dab80-deb3-11e8-95af-214a9d8db8b5.png)

###### `tickets.effects.ts`
![image](https://user-images.githubusercontent.com/210413/47975472-94f8e300-e073-11e8-939b-8fe32e36c627.png)




<br/>


----

<br/>

### Investigate

* Why did we use `ticketsQuery.getTicketAsEntities(state)`? 
* What are the benefits?

> Be prepared to discuss this? 


<br/>

### Running the Application with REST Delays

*  Open the **Customer Portal** application with the browser: http://localhost:4203
*  Confirm the **Node Server** is running with browser page:  http://localhost:3000/api/tickets

Run the following command(s) in individual terminals:

```console
yarn server --throttle
```

```console
yarn customer-portal -- -o
```

> The `--throttle` option introduces random delays in the REST server responses... so the in-progress spinner becomes much more obvious.


<br/>

----

<br/>

## Challenge Lab

Currently the Search Tickets view does not remember the search criteria.

Add TicketSearch state to to the **tickets-state** library:

```ts
export interface SearchCriteria {
   searchTerm ?: string,
   assignedToUser ?: string;
};
```

Then update TicketState: 

```ts
export interface TicketsState extends EntityState<Ticket> {
  searchCriteria: SearchCriteria;
  selectedId: number;
  loading: boolean;
  error: any;
}
```

Then update the Reducer, Effects, Actions, and Facade to manage and track changes to search criteria. Whenever the user routes to *Search Tickets*, the last used search criteria and search results should be shown.

## Next Lab

You have finished the **Nx Workshop: NgRx Course**. Congratulations. 
