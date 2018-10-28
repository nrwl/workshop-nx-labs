# Lab Exercise: Add Subscriptions to Ticket Search Form

## Time: 15 minutes

## Scenario

In this application, we have search features and a crude dropDown `assignedToUser` menu.

![rxjs1 0](https://user-images.githubusercontent.com/210413/47622033-f1855c80-dacd-11e8-9ec0-1d26a90b3456.jpg)



The dropDown menu should dynamically populate as the user types.

Whenever the customer types in the `assignedToUser` input field, a RESTful service call should be dispatched to load all *matching* users using the current user-search criteria.


Let's start with a search for Tickets matching the letter '**a**' for assigned users matching **nrwl** in the "Assigned To:" field. Currently the ticket search is not automatic... you must click the **Search** button.


<br/>

----

You should NOT use the `async` pipe. For now, you will manually subscribe to `assignedToUser` value changes. As such you will also need to manually unsubscribe.

----

<br/>

### Code Instructions

##### In `search-tickets.component.ts`

 1. subscribe to `assignedToUser.valueChanges` and make a call to the `UserService.users` method (pass in the `value` for the search term). Subscribe to that Observable and update the `users` property with the server results.
 2. Save the `subscription` reference and implement `OnDestroy` to unsubscribe from the subscription.
 3. The Ticket Search will display a list of matching tickets using `searchResults$ | async`. When the `submit` button is clicked, search for tickets using `TicketService.searchTickets`. You can use the `FormControl.value` property to get the value from the form field (example: `this.searchTerm.value`).
 
##### In `search-tickets.component.html`

1. Use an `*ngFor` template directive to display the list of users for the suggest-on-type feature. Make use of the `user.fullName` property for both the label the value to pass to the `setAssignedToUser` class method.

<br/>

### Investigate

Check out the `network` tab in the browser dev tools as you type in the "Assigned To:" field.

![networktraffic](https://user-images.githubusercontent.com/210413/35155098-37725cbc-fcf2-11e7-9466-d852d6722873.jpg)

Be prepared to discuss what you notice!

<br/>

### Code Snippets

###### `search-tickets.component.ts`

![rxjs1 2](https://user-images.githubusercontent.com/210413/47622136-660ccb00-dacf-11e8-8e62-2cbc910fea9f.jpg)

###### `search-tickets.component.html`

![rxjs1 1](https://user-images.githubusercontent.com/210413/47622122-2e9e1e80-dacf-11e8-8f0a-9616c55943f8.jpg)



<br/>

### Bonus:

Replace your custom drop down with [Material **Select** component](https://material.angular.io/components/select/examples).


<br/>

----

<br/>

### Running the Application

Run the following command(s) in individual terminals:

```console
npm run server
npm run customer-portal
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
