# Lab: Add Subscriptions to Ticket Search Form

## Scenario

## Instructions
1. Subscribe to `assignedToUser.valueChanges` in `ngOnInit` and make a call to the `UserService.users` method (pass in the `value` for the search term). Subscribe to that and wire up the `users` class field to the results.
1. Capture the `valueChanges` subscription into a class field and implement `OnDestroy` to unsubscribe from the subscription.
1. Set `searchResults$` class field equal to a call to `TicketService.searchTickets` in the `submit` class method.
1. Use an `ngFor` to display the list of users for the suggest on type. Make use of the `User.fullName` for display and for the value to pass to the `setAssignedToUser` class method.
1. Bring up the customer portal project in the browser (make sure the server is running) and search for the letter **a**. Type **nrwl** in the "Assigned To:" field to see the suggest on type.
1. Check out the `network` tab in the browser dev tools as you type in the "Assigned To:" field. What do you notice?

## Next Lab
Go to []()