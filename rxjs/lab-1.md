# Lab Exercise: Add Subscriptions to Ticket Search Form

## Time: 15 minutes

## Scenario

In this application, we have search features and a crude dropDown `assignedToUser` menu. 

![lab1_snapshot](https://user-images.githubusercontent.com/210413/35134346-67e08b64-fc9b-11e7-9756-aec2e5e38a7f.jpg)

The dropDown menu should dynamically populate as the user types.

Whenever the customer types in the `assignedToUser` input field, a RESTful service call should be dispatched to load all *matching* users using the current user-search criteria. 


Let's start with a search for Tickets matching the letter '**a**' for assigned users matching **nrwl** in the "Assigned To:" field. Currently the ticket search is not automatic... you must click the **Search** button.


<br/>

----

You should NOT use the `async` pipe. For now, you will manually subscribe to `assignedToUser` value changes. As such you will also need to manually unsubscribe.

----

<br/>

### Code Instructions

1. In `search-tickets.component.ts`, subscribe to `assignedToUser.valueChanges` and make a call to the `UserService.users` method (pass in the `value` for the search term). Subscribe to that and wire up the `users` class field to the results.

  ###### libs/ticket-list-view/src/search-tickets/search-tickets.component.ts
  
  ```typescript
  ngOnInit() {
    this.subscription = this.assignedToUser... // Update this code
  }
  ```

<br/>

2. In `search-tickets.component.ts`, save the `subscription` reference and implement `OnDestroy` to unsubscribe from the subscription.

  ```typescript
  ngOnDestroy() {
    // <YOUR - CODE - HERE>
  }
  ```

<br/>

3. The Ticket Search will display a list of matching tickets using `searchResults$ | async`. In `search-tickets.component.ts`, when the `submit` button is clicked, search for tickets using `TicketService.searchTickets`. You can use the `FormControl.value` property to get the value from the form field (example: `this.searchTerm.value`).

  ```typescript
  submit() {
      this.searchResults$ = this.ticketService.searchTickets(<TICKET-SEARCH-TERM>, <ASSIGNED-USER>);
  }
  ```
  
<br/>  

4. In `search-tickets.component.html`, use an `*ngFor` template directive to display the list of users for the suggest-on-type feature. Make use of the `user.fullName` property for both the label the value to pass to the `setAssignedToUser` class method.

  ###### libs/ticket-list-view/src/search-tickets/search-tickets.component.html

  ```html
    <ul>
      <li *ngFor="let user of users" (click)=""> 
          
      </li>
    </ul>
  ```
  
<br/>

### Investigate

Check out the `network` tab in the browser dev tools as you type in the "Assigned To:" field. 

![networktraffic](https://user-images.githubusercontent.com/210413/35155098-37725cbc-fcf2-11e7-9466-d852d6722873.jpg)

Be prepared to disucss what you notice!

<br/>

----

<br/>

### Running the Application

Run the following command(s) in individual terminals:

```console
npm run server & npm run customer-portal
```


*  Open the **Customer Portal** application with the browser: http://localhost:4203 
*  Confirm the **Node Server** is running with browser page:  http://localhost:3000/api/tickets

If you already have one(s) running and you need to restart, you can stop the run with `ctrl+c`.

#### Restarting the App Server

Sometimes a change to TypeScript interfaces or adding new `*.ts` files <u>will not get picked up</u> by the watch processes. In such cases, you may need to stop/restart these... if you feel your code is correct but you are getting an error.


<br/>

----

<br/>

### Next Lab

Go to RxJS Lab #2: [Throttle Assigned to User Field and Transform](lab-2.md)
