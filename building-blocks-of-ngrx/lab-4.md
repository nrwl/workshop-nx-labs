# Lab: Create a Feature State for Ticket Comments

## Scenario
Creating feature state for NgRx is very similar to root state, with a few different configurations and selector logic. But feature state can be lazy loaded, making it a good fit for lazy loaded modules. They also allow you to flatten your store structure and group related state together.

Tickets have comments that we'd like to display in the ticket details. As of right now the ticket details is part of the ticket list view lib. But in the near future it is possible we may want to split that out into its own lib so it can be lazy loaded if a user decides to drill down to a ticket. We can set up the comments data in the state to be a feature state so that it is not only ready to be lazy loaded in the future, but is also isolated in its own segment and can be managed independently.

Use the Nx schematic for ngrx to create the boilerplate code for a feature state for comments and use that in the ticket details component to display the comments for a ticket. Make use of NgRx Entity in the same fashion as the tickets state from last lab.

Since the ticket details is already working with the tickets state, a solution is needed for bridging the data model for the state. But that can be accomplished with a little TypeScript interface magic.

## Instructions
1. Create a **comments-state** lib using the `lib` schematic.

1. Create a **comments** state using the `ngrx` schematic. Provide the `module` option to point to the **comments-state** module (do not use the `root` flag).

1. Configure all of the pieces of state (interfaces, init, reducers, effects). Use the **ngrx/entity** library to work with the comments data. Use the existing `TicketComment` interface found in the **data-models** lib.

1. Import the **comments-state** module into the **tickets-list-view** module.

1. Create a new interface in the **tickets-list-view** lib `+state` folder that bridges the `tickets` and `comments` state features.

1. Use the new interface in the ticket details component for the `Store` generic type.

1. Dispatch an action to load the comments for the ticket in the component.

1. Select the comments from the state and use them in the component.

## Viewing in the Browser
Run the following command(s) in individual terminals:
- `npm run server`
- `npm run customer-portal`

Open up the browser to:
- http://localhost:4203 (customer portal app)

If you already have one(s) running and you need to restart, you can stop the run with `ctrl+c`.

*(Note: sometimes a change to TypeScript interfaces will not get picked up by the watch so you may need to stop/restart these if you feel your code is correct but you are getting an error)*

If you have the Redux DevTools extension installed, open that up either under the dev tools panel or via the icon in the top browser bar. Usually you will have to have this open before hitting the site for the data to load, so if you don't see data try refreshing the page.
