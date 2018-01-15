# Lab: 

## Scenario

## Instructions
1. Use the `pipe` method on the `assignedToUser.valueChanges` observable.
1. Make use of the `debounceTime` and `distinctUntilChanged` operators for the `assignedToUser` to throttle the user lookup.
1. Use the `filter` operator on `assignedToUser` to only allow value strings with a length greater than zero.
1. Use the `tap` operator on `assignedToUser` to set the `users` class field to `null` when the length of `value` is zero.
1. Use `pipe` with the `map` operator on the `UserService.users` observable to transform each user object to just the `fullName` property (Hint: you will need to do an array `map` within the `map` operator). Update the `users` class field to be an array of strings and update the template `ngFor` logic for the suggest on type.

## Next Lab
Go to []()