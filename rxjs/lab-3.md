# Lab: Use SwitchMap

## Time: 20 minutes

## Scenario

In the last lab, we fixed the server-thrashing performance issue(s)!

<br/>

![rxjs1 0](https://user-images.githubusercontent.com/210413/47622033-f1855c80-dacd-11e8-9ec0-1d26a90b3456.jpg)

But **now** we have some subtle race-conditions to fix!  The server may respond with out-of-order responses to the AssignedUser query. What we need to do is cancel the previous query/search before we issue another new query to the server!

Let's fix these **race-condition issues**!

<br/>

----

## Instructions

##### In `search-tickets.component.ts`


1. Refactor the `assignedToUser.valueChanges` pipe of operators to remove the `tap` operator.
2. Use the `switchMap` operator in the `assignedToUser.valueChanges` pipe and return the call to `UserService.users` from that. Make sure it still has the `map` operator for it!
3. Change the `users` class field to be an observable
  >  Note the use of the `$` suffix in `users$`. This is a recommended notation standard for all observable variables. Also note that this is an observable of a **string[]**. Why is that ?
4. Remove the `subscribe` to the `valueChanges` that contained the `UserService` call.
5. Get rid of the `subscription` class field and the call to `unsubscribe()` in `ngOnDestroy`.
6. Update the template to use the `async` pipe for the users.

<br/>

### Bonus Exercise

When the AssignedUsers search criteria field is empty, how can you auto-clear the dropDown menu? Please do NOT use the `tap()` operator. Hint use `Observable.of()`

### Code Snippets

###### `search-tickets.component.ts`

![rxjs3 1](https://user-images.githubusercontent.com/210413/47622584-b5092f00-dad4-11e8-8482-2edf7ee16987.jpg)




<br/>

----

<br/>

### Next Lab

Go to RxJS Lab #4: [Create a Ticket Timer Observable](lab-4.md)
