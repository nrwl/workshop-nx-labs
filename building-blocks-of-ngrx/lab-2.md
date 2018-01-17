# Lab: Refactor Tickets State to Use Key/Value Object

## Scenario

## Instructions
1. Refactor the `TicketsStateModel` tickets property to be an object with key/value instead of an array. `{[key: number]: Ticket}`
1. Add a property for `ids` that is an array of numbers.
1. Refactor the tickets state model init to set `tickets` to an empty object and add the `ids` property.
1. Refactor the tickets state model reducer to work with the tickets object instead of an array of tickets.
1. Refactor the tickets list component to select the `ids` and map to the tickets from the `tickets` object. Make sure you keep the logic for filtering open tickets in there.
1. Refactor the ticket details component to select the ticket based on the ticket object key.

## Next Lab
Go to [Refactor Tickets State to use NgRx Entity](building-blocks-of-ngrx/lab-3.md)