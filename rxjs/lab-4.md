# Lab: Create a Ticket Timer Observable

## Scenario

## Instructions
1. Use the Angular CLI schematics to generate a new `TicketTimer` service in the `ticket-list-view` lib (make sure you add it to the providers for the ticket list view module by using the `--module` flag).
1. Create a private class field for a timer and set that equal to a call to `Observable.create`.
1. Pass that in a function literal with an `observer` arguement. In the body, set up a count variable and use `setInterval` to increment it every `1000ms`. Make a call to `observer.next` in the setInterval callback and send that the counter value.
1. Capture the handle to the `setInterval` and use it in teardown logic to clean it up (have the function literal return a function that clears the interval with `clearInterval`).
1. Create a getter class field and return the private timer class field.
1. Inject the service into the `TicketDetailsComponent` and set the `timer$` class field to the getter class field from `TicketTimer` service when the "Start a Timer" button is clicked.
1. Open up the customer portal in the browser, go to a ticket and start a timer. Breakpoint (or `console.log`) in the teardown logic and navigate away from the ticket to confirm the teardown works.
1. (Bonus: set up an array of `Observable<number>` as timers and push the `TicketTimer` service timer into it, then update the template to `ngFor` the timers and use the async pipe to display each timer value. What is this doing? What happens when you navigate away from the ticket?)

## Next Lab
Go to [Track Tickets to Work With a Multi-Cast Observable](lab-5.md)