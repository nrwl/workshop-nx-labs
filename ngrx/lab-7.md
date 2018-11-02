# NgRx Lab 7: Select Action and Loading Indicators

### Scenario

Each time the user routes to the TicketDetails view, a LoadTicket action requests a refresh from the server. 
Let's instead *select* the ticket in the TicketList view and then query for the **selectedTicket** when we route to the TicketDetails view. 
And if the ticket is not available in our NgRx state, we will auto-load it.

> Note this solution will use an NgRx **Action Decider** to conditionally load ticket details remotely.

Also, let's simulate a delayed server responses and show a loading/in-progress UI indicator while we are loading REST ticket data.
 
### Code Instructions

<br/>

----
  

#### Part A: 'Loading Indicators' feature

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
![tickets.reducer.ts](https://user-images.githubusercontent.com/210413/47938571-8f07d400-deb2-11e8-8ec2-5792f51c0539.png)

###### `ticket-list.component.html`
![ticket-list.component.html](https://user-images.githubusercontent.com/210413/47938584-97f8a580-deb2-11e8-9727-6db09c34e4f1.png)

###### `ticket-details.component.html`
![ticket-details.component.html](https://user-images.githubusercontent.com/210413/47938591-9e871d00-deb2-11e8-95bc-766713786cb4.png)


<br/>

----
  
<br/>

#### Part B: SelectTicket feature

<br/>

1. In `tickets.actions.ts`, add a `SelectTicket` enum and action class to `tickets.actions.ts` 
2. In `tickets.reducer.ts`, add a `case TicketActionTypes.SELECT_TICKET: {...}` to update the `selectedId` state value.

##### In `tickets.facade.ts`

1. Create a `selectedTicket$` observable using `ticketsQuery.getSelectedTicket`
2. Replace `loadTicketById()` with `selectTicket()` and dispatch a `SelectTicket` action.

##### In `tickets.effects.ts`

1. Create a `@Effect() selectTicket$` with a `run` callback that conditionally emits a `LoadTicket()` action. 
  > Use `ticketsQuery.getTicketAsEntities(state)` to get all currently loaded tickets and check it the selected ticket has already been loaded. 


##### In `ticket-details.component.ts`

1. Use the TicketFacade `selectedTicket$` query:  `ticket$ = this.facade.selectedTicket$`
2. Replace the use of `facade.entities$.pipe(...)` with `this.facade.selectTicket(id);`


<br/>

##### **Code Snippets**

###### `tickets.actions.ts`
![tickets.actions.ts](https://user-images.githubusercontent.com/210413/47938930-9380bc80-deb3-11e8-9ee2-78664af6edef.png)

###### `tickets.reducer.ts`
![tickets.reducer.ts](https://user-images.githubusercontent.com/210413/47938937-99769d80-deb3-11e8-957d-268d1b4482bb.png)

###### `tickets.facade.ts`
![tickets.facade.ts](https://user-images.githubusercontent.com/210413/47938946-a09dab80-deb3-11e8-95af-214a9d8db8b5.png)

###### `tickets.effects.ts`
![tickets.effects.ts](https://user-images.githubusercontent.com/210413/47939902-de500380-deb6-11e8-89e3-d4089a9f48f6.png)


<br/>


----

<br/>

### Investigate

* Why did we use `ticketsQuery.getTicketAsEntities(state)`? 
* What are the benefits?

> Be prepared to discuss this? 


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

You have finished the **Nx Workshop: NgRx Course**. Congratulations. 
