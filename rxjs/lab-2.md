# RxJS Lab 2: Throttle Search Requests

### Scenario

While searching is working for users and tickets, we have a performance issue!

![rxjs1 0](https://user-images.githubusercontent.com/210413/47622033-f1855c80-dacd-11e8-9ec0-1d26a90b3456.jpg)

For each change in the AssignedUsers search criteria, we are thrashing the server:

*  We are not waiting until the user appears to have finished changing the criteria.
*  We are querying the server with possible same query as the most recent, previous query.


Let's fix these **performance issues**! 😱 

<br/>

----

<br/>

## Instructions

##### In `search-tickets.component.ts`

1. Use the `pipe` method on the `assignedToUser.valueChanges` observable.
2. Import and use the **`debounceTime`** and **`distinctUntilChanged`** operators for the `assignedToUser` observable... to manage and throttle the user lookup queries. A good suggested debounce time is **500** milliseconds, although feel free to try out different values and see what the user experience is like!
3. Use the **`filter`** operator on `assignedToUser` to only allow value strings with a length greater than zero.
4. Use the **`tap`** operator on `assignedToUser` to set the `users` class field to `null` when the length of `value` is zero.
5. Use `pipe` with the **`map`** operator on the `UserService.users` observable to transform each user object to just the `fullName` property; this is known as *extracting a property value*. Update the `users` class field to be an array of strings and update the template `ngFor` logic for the suggest on type.
  >  Hint: you can use `Array.map()` within the observable `map` operator.

##### In `search-tickets.component.html`

1. Change the name of the templateRef variable from `#users` to `#dropDown`.
2. Update the variable name `usersFound` to be `users`.
  > Notice that now we have `users: string[]` instead of `usersFound: User[]`.
  
### Code Snippets

###### `search-tickets.component.ts`

![rxjs2 1](https://user-images.githubusercontent.com/210413/52433219-327c0c80-2ad2-11e9-953d-784402e6f221.png)

###### `search-tickets.component.html`

![rxjs2 2](https://user-images.githubusercontent.com/210413/52433221-327c0c80-2ad2-11e9-89cc-389eac3f6897.png)

<br/>

----

<br/>


### Investigate

This ^ code works great to manage and control REST server queries.

There is, however, a **bad practice** code implementation here.. and an actual super-subtle **race-condition** bug 😜! Be prepared to discuss it! (Don't cheat and look ahead! 🤗)

<br/>

## Next Lab

Go to RxJS Lab #3: [Use SwitchMap](lab-3.md)
