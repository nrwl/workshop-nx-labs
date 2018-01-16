# Lab: 

## Scenario

## Instructions
1. Create a **comments-state** lib using the `lib` schematic.
1. Create a **comments** state using the `ngrx` schematic. Provide the `module` option to point to the **comments-state** module (do not use the `root` flag).
1. Configure all of the pieces of state (interfaces, init, reducers, effects). Use the **ngrx/entity** library to work with the comments data.
1. Import the **comments-state** module into the **tickets-list** module.
1. Create a new interface in the **tickets-list** lib that bridges the `tickets` and `comments` state features.
1. Use the new interface in the ticket details component for the `Store` generic type.
1. Dispatch an action to load the comments for the ticket in the component.
1. Select the comments from the state and use them in the component.

## Next Lab
Go to []()