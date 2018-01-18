# Lab: Refactor Tickets State to Use Key/Value Object

## Scenario
The ticket state code is currently storing the tickets as an array. The customer portal app already has the need to pull up individual tickets, and it will eventually need to get updated to support editing tickets. Finding items in an array can be painful and a potential performance hit.

Refactor the tickets array in state to use a key/value object approach. Add a new property to keep track of sort order, and update the reducers and select logic to support the new store structure. When refactoring the reducers, make sure you are "changing" state and not "mutating" state!

## Instructions
1. Refactor the `TicketsStateModel` tickets property to be an object with key/value instead of an array.  
`{[key: number]: Ticket}`

1. Add a property for `ids` that is an array of numbers.

1. Refactor the tickets state model init to set `tickets` to an empty object and add the `ids` property.

1. Refactor the tickets state model reducer to work with the tickets object instead of an array of tickets.

1. Refactor the tickets list component to select the `ids` and map to the tickets from the `tickets` object. Make sure you keep the logic for filtering open tickets in there.

1. Refactor the ticket details component to select the ticket based on the ticket object key.

## Viewing in the Browser
Run the following command(s) in individual terminals:
- `npm run server`
- `npm run customer-portal`

Open up the browser to:
- http://localhost:4203 (customer portal app)

If you already have one(s) running and you need to restart, you can stop the run with `ctrl+c`.

*(Note: sometimes a change to TypeScript interfaces will not get picked up by the watch so you may need to stop/restart these if you feel your code is correct but you are getting an error)*

If you have the Redux DevTools extension installed, open that up either under the dev tools panel or via the icon in the top browser bar. Usually you will have to have this open before hitting the site for the data to load, so if you don't see data try refreshing the page.

## Next Lab
Go to [Refactor Tickets State to use NgRx Entity](lab-3.md)