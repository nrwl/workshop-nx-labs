# Lab: 

## Scenario

## Instructions
1. Use the Angular CLI schematics to generate a new `TicketTimer` service in the `ticket-list-view` lib.
1. Create a private class field for a timer and set that equal to a call to `Observable.create`.
1. Pass that in an object literal with an `observer` arguement. In the body, set up a count variable and use `setInterval` to increment it every `1000ms`. Make a call to `observer.next` in the setInterval callback and send that the counter value.
1. Capture the handle to the `setInterval` and use it in teardown logic to clean it up.
1. Create a getter class field and return the private timer class field.
1. Inject the service into the `TicketDetailsComponent` and subscribe to the getter class field from `TicketTimer` service in the "Track Time" click method. Set a class field for the timer value in the `subscribe` and update the template to show it. Don't forget to capture the subscription and unsubscribe!

## Next Lab
Go to []()