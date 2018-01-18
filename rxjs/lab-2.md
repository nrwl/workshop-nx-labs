# Lab: Throttle Assigned to User Field and Transform

## Scenario

## Instructions
1. Use the `pipe` method on the `assignedToUser.valueChanges` observable.

1. Make use of the `debounceTime` and `distinctUntilChanged` operators for the `assignedToUser` to throttle the user lookup.

1. Use the `filter` operator on `assignedToUser` to only allow value strings with a length greater than zero.

1. Use the `tap` operator on `assignedToUser` to set the `users` class field to `null` when the length of `value` is zero.

1. Use `pipe` with the `map` operator on the `UserService.users` observable to transform each user object to just the `fullName` property (Hint: you will need to do an array `map` within the `map` operator). Update the `users` class field to be an array of strings and update the template `ngFor` logic for the suggest on type.

## Viewing in the Browser
Run the following command(s) in individual terminals:
- `npm run server`
- `npm run customer-portal`

Open up the browser to:
- http://localhost:4203 (customer portal app)

If you already have one(s) running and you need to restart, you can stop the run with `ctrl+c`.

*(Note: sometimes a change to TypeScript interfaces will not get picked up by the watch so you may need to stop/restart these if you feel your code is correct but you are getting an error)*

## Next Lab
Go to [Use SwitchMap](lab-3.md)