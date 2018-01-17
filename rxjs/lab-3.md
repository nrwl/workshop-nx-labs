# Lab: Use SwitchMap

## Scenario

## Instructions
1. Refactor the `assignedToUser.valueChanges` pipe of operators to remove the `tap` operator.
1. Use the `switchMap` operator in the `assignedToUser.valueChanges` pipe and return the call to `UserService.users` from that. Make sure it still has the `map` operator for it!
1. Remove the `subscribe` to the `valueChanges` that contained the `UserService` call.
1. Get rid of the `subscription` class field and the call to unsubscribe.
1. Change the `users` class field to be an `Observable<string[]>`, set the call to `valueChanges` to that class field.
1. Update the template to use the `async` pipe for the users.
1. (Bonus: figure out how to clear the users when value is empty)

## Next Lab
Go to [Create a Ticket Timer Observable](lab-4.md)