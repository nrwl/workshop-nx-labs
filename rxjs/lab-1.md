# Lab: Add Subscriptions to Ticket Search Form

## Scenario

In this application, we have search features and a crude dropDown `assignedToUser` menu that should dynamically populate as the user types.

![lab1_snapshot](https://user-images.githubusercontent.com/210413/35134346-67e08b64-fc9b-11e7-9756-aec2e5e38a7f.jpg)


Whenever the customer types in the `assignedToUser` input field, a RESTful service call should be dispatched to load all *matching* users using the current field value. A valid response from the server should be saved to `this.users` and the template should update to show the dynamic query results.

Search for Tickets matching the letter **a**. Search for assigned users matching **nrwl** in the "Assigned To:" field. Click **Search**.

> Note: you should NOT use the `async` pipe. For now, you will manually subscribe to `assignedToUser` value changes. As such you will also need to manually unsubscribe.

<br/><br/>

----

### Instructions

1. Subscribe to `assignedToUser.valueChanges` and make a call to the `UserService.users` method (pass in the `value` for the search term). Subscribe to that and wire up the `users` class field to the results.

  ```js
  ngOnInit() {
    this.subscription = this.assignedToUser... // Update this code
  }
  ```

<br/>

2. Save the `subscription` reference and implement `OnDestroy` to unsubscribe from the subscription.

3. The Ticket Search will display a list of matching tickets using `searchResults$ | async`. When the `submit` button is clicked, search for tickets using `TicketService.searchTickets`.

  ```js
  submit() {
      this.searchResults$ = this.ticketService.searchTickets(<TICKET-SEARCH-TERM>, <ASSIGNED-USER>);
  }
  ```
  
<br/>  

4. Use an `ngFor` to display the list of users for the suggest on type. Make use of the `User.fullName` for display and for the value to pass to the `setAssignedToUser` class method.

<br/>

##### Tip  

Check out the `network` tab in the browser dev tools as you type in the "Assigned To:" field. 

Be prepared to disucss what you notice!

<br/><br/>



----

### Running the Application

Run the following command(s) in individual terminals:

```console
npm run customer-portal && npm run server
```


*  Open the **Customer Portal** application with the browser: http://localhost:4203 
*  Confirm the **Node Server** is running with browser page:  http://localhost:3000/api/tickets

If you already have one(s) running and you need to restart, you can stop the run with `ctrl+c`.

>  Note: sometimes a change to TypeScript interfaces <u>will not get picked up</u> by the watch. In such cases, you may need to stop/restart these... if you feel your code is correct but you are getting an error.


<br/><br/>

----

### Next Lab

Go to [Throttle Assigned to User Field and Transform](lab-2.md)
