# Lab: Add Subscriptions to Ticket Search Form

## Scenario

## Instructions
1. Subscribe to `assignedToUser.valueChanges` in `ngOnInit` and make a call to the `UserService.users` method (pass in the `value` for the search term). Subscribe to that and wire up the `users` class field to the results.

1. Capture the `valueChanges` subscription into a class field and implement `OnDestroy` to unsubscribe from the subscription.

1. Set `searchResults$` class field equal to a call to `TicketService.searchTickets` in the `submit` class method.

1. Use an `ngFor` to display the list of users for the suggest on type. Make use of the `User.fullName` for display and for the value to pass to the `setAssignedToUser` class method.

1. Bring up the customer portal project in the browser (make sure the server is running) and search for the letter **a**. Type **nrwl** in the "Assigned To:" field to see the suggest on type.

1. Check out the `network` tab in the browser dev tools as you type in the "Assigned To:" field. What do you notice?

## Viewing in the Browser
Run the following command(s) in individual terminals:
- `npm run server`
- `npm run customer-portal`

Open up the browser to:
- http://localhost:4203 (customer portal app)

If you already have one(s) running and you need to restart, you can stop the run with `ctrl+c`.

*(Note: sometimes a change to TypeScript interfaces will not get picked up by the watch so you may need to stop/restart these if you feel your code is correct but you are getting an error)*

## Next Lab
Go to [Throttle Assigned to User Field and Transform](lab-2.md)