# RxJS Lab 6: Combining Observable Streams


## Scenario

In this last, we will use the concepts combining multiple observable streams.

![startwork](https://user-images.githubusercontent.com/210413/52439186-8d1c6500-2ae0-11e9-8cbf-5e2354b77c59.jpg)

Currently the application will auto search for users matching search criteria in the 'Assigned to:' input field.
Let's remove the 'Submit' button and auto-search for matching tickets based on values in the 'Find Tickets' and 'Assigned To:' fields.

We will need to use the `combineLatest` creation operator to gather values from two (2) observable streams;

----

This is a optional **Bonus Lab** based on time and developer interest

----

## Instructions

##### In `search-tickets.component.html`, 

1. Remove the `<button>`

##### In `search-tickets.component.ts`, 

1. Since we will throttle both input controls, create a `function throttle(source$: Observable<string>)` that applies `debounceTime()`, `distinctUntilChange()`, and startWith()` operators.

> Be prepared to talk about why the `startWith()` operator is needed.

2. Update the `searchResults$` to use the `combineLatest()` operator
```floobits
  this.searchResults$ = combineLatest(searchBy$, users$).pipe(... );
```

<br/>

---

The important lesson here is the joining of two input streams to auto-call `ticketService.searchTickets()`

---

### Code Snippets

###### `search-ticker.component.ts`

![search-ticket.component.ts](https://user-images.githubusercontent.com/210413/52439830-239d5600-2ae2-11e9-9820-946574ae1db3.png)


<br/>

----

<br/>

### Next Lab

Go to **RxJS Lab #7: [RxJS + Facades](/rxjs/lab-7.md)**
