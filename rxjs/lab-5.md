# Lab: 

## Scenario

## Instructions
1. In the `TicketTimer` service, create a private class field for keeping an array of ticket ids (a string) to work.
1. Add a private class field for tickets to work. Set that to a new `BehaviorSubject` with an initial value of the private class field for ticket ids to work.
1. Create a getter class field for the tickets to work and return the private class field.
1. Create a class method to add ticket id to work that takes in a string and adds the id to the ticket ids to work private calss field if it is not already in the array and calls the `next` method off of the private class field for tickets to work and pass a copy of the ticket ids to work.
1. Update the `TicketDetailComponent` method that marks ticket to work and make a call to the ticket timer service method to add a ticket id to work, passing in the ticket id.
1. Set up a class field for the tickets to work observable from the ticket timer service and use it to toggle a css class named `marked` on the `ticket-header` element in the ticket details template (think about how you can use operators like `filter` and `map` to transform the array of ids to something you can use in the template as a `boolean` check).
1. Update the `TicketListComponent` to inject the `TicketTimer` service and wire up the tickets to work observable in the template with the async pipe to display a count of the total number of tickets to work.
1. (Bonus: add a way to remove a ticket id to work so they can be toggled on and off from the ticket details view.)

## Next Lab
Go to []()