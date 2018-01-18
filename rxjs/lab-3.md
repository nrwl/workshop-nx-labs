# Lab: Use SwitchMap

## Scenario

## Instructions
1. Refactor the `assignedToUser.valueChanges` pipe of operators to remove the `tap` operator.

1. Use the `switchMap` operator in the `assignedToUser.valueChanges` pipe and return the call to `UserService.users` from that. Make sure it still has the `map` operator for it!

1. Remove the `subscribe` to the `valueChanges` that contained the `UserService` call.

1. Get rid of the `subscription` class field and the call to unsubscribe.

1. Change the `users` class field to be an `Observable<string[]>`, set the call to `valueChanges` to that class field.

1. Update the template to use the `async` pipe for the users.

1. (Bonus: figure out how to clear the users when value is empty.)

## Viewing in the Browser
Run the following command(s) in individual terminals:
- `npm run server`
- `npm run customer-portal`

Open up the browser to:
- http://localhost:4203 (customer portal app)

If you already have one(s) running and you need to restart, you can stop the run with `ctrl+c`.

*(Note: sometimes a change to TypeScript interfaces will not get picked up by the watch so you may need to stop/restart these if you feel your code is correct but you are getting an error)*

## Next Lab
Go to [Create a Ticket Timer Observable](lab-4.md)