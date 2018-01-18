# Lab: Refactor Tickets State to use NgRx Entity

## Scenario
NgRx entity is designed to take care of data management in your state in a way that is efficient and performant. It handles the store structure part and provides an easy way to write reducer logic.

Refactor the tickets state to use Entity instead of the hand crafted version you wrote last lab. Update the interface, initial state and reducer. Introduce selector functions as they are needed to get to the entities in the state. Take note how some of this will be easier to work with (and provide some additional mutation safety), but for other parts it will add some complexity.

## Instructions
1. Update the `TicketsStateModel` interface to extend from `EntityState` and give it a generic of type `Ticket`. Remove the properties in it as they will be handled by the `EntityState`.
1. Use the `createEntityAdapter` to create a new `ticketsStateAdapter` constant in the `tickets-state-model.init.ts` file and export that.
1. Use the `getInitialState` method from the adapter to set the `ticketsStateModelInitialState` initial state object.
1. Create some selectors using the adapter `getSelectors` method in the `tickets-state-model.init.ts` file.
```typescript
const {
  selectAll: selectAllTickets,
  selectEntities: selectTicketEntities
} = ticketsStateAdapter.getSelectors();
```
5. Create selectors that can be used by components to query the tickets from the state. Make a feature selector for the `TicketsStateModel`. Use that to make selectors for tickets and tickets as entities.
```
export const selectTicketState = createFeatureSelector<TicketsStateModel>('ticketsStateModel');
export const selectTickets = createSelector(selectTicketState, selectAllTickets);
export const selectTicketAsEntities = createSelector(selectTicketState, selectTicketEntities);
```
6. Export the `selectTickets` and `selectTicketsAsEntities` from the index.ts file in the **tickets-state** lib to make them public.
1. Refactor the reducer to use the adapter `addAll` method to set the list of tickets and the `addOne` to set an individual ticket.
1. Update the ticket list component to use the `selectTickets` selector instead of the function literal of `s => s.ticketsStateModel`.
1. Update the ticket details component to use the `selectTicketAsEntities` selector instead of the function literal of `s => s.ticketsStateModel.tickets`.

## Next Lab
Go to [Create a Feature State for Ticket Comments](lab-4.md)