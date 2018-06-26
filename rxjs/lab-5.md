# Lab: Track Tickets to Work With a Multi-Cast Observable

## Time: 20 minutes

## Scenario

In this last, we will use the concepts of UniCast and MultiCast observables and explore a solution using a `BehaviorSubject` .

![startwork](https://user-images.githubusercontent.com/210413/35168754-c42e14b6-fd1f-11e7-93e8-af0836b3ff3c.jpg)

Using a **BehaviorSubject** to cache the current list of tickets with "work" status is useful for future subscribers... as they will then get the updated, current list.


## Instructions
1. In the `TicketTimerService`, create a private class field for cache a list of 'working' ticket ids.

  *  Also add a private class field for tickets to work.
     *  Instantiate to a new `BehaviorSubject` with an initial value of the current empty `_ticketsIdsToWork` list.
  *  Create a accessor (aka getter) field to publish the private tickets-to-work list.

 ###### libs/ticket-list-view/src/lib/ticket-timer.ts

  ```typescript
    export class TicketTimerService {
      private _ticketIdsToWork = [];
      private _ticketsToWork$  = new BehaviorSubject(this._ticketIdsToWork);

     get ticketsToWork$() {
        <RETURN TO-WORK LIST>
      }
    }
  ```

  <br/>

2. In the `TicketTimerService`, create an `addTicketIdToWork()` class method to add ticket id to the internal, private list and then use the *BehaviourSubject* `next()` to announce the changes to external observers.

  ###### libs/ticket-list-view/src/lib/ticket-timer.ts

  ```typescript
    export class TicketTimerService {

      addTicketIdToWork(id:string) {

        <SAVE TICKET ID; NO DUPLICATES>
        <ANNOUNCE CHANGE TO OBSERVERS>
      }
    }
 ```

 >  Note: you should announce the changes using a clone of the list. **Question:** Why?


3. In the `ticket-details.component.ts`, this view component has a click handler on the header to call `markToWork()`. Update `markToWork()` to make a call to the ticket timer service method to add a ticket id to work.

  ###### libs/ticket-list-view/src/lib/ticket-details/ticket-details.component.ts

  ```typescript
     export class TicketDetailsComponent {

       markToWork(ticketId: string) {
         <CALL TICKET TIMER SERVICE TO ADD TICKET ID>

       }
    }
  ```

4. In (3) above we added code to add a ticket to our 'to-work' list. Now we need to configure (using observables) a watch to update the header color when the current ticket is in that 'to-work' list.

  ###### libs/ticket-list-view/src/lib/ticket-details/ticket-details.component.ts

  ```typescript
     export class TicketDetailsComponent {
        // ... other code here
        markedToWork$: Observable<boolean>;

        ngOnInit() {
          this.route.params.subscribe(params => {
            const id = +params['id'];
            // .... current code

            const allMarkedTickets$ = this.ticketTimerService.ticketsToWork$;
            this.markedToWork$ = allMarkedTickets$.pipe(

              <ADD CODE HERE TO TRANSFORM VALUE TO BOOLEAN BASED ON TICKET ID IN LIST OF TICKETS>

            );
          });
        }
    }
  ```

In `ticket-details.component.html`, use class data binding to update CSS header stylings when the ticket is "marked to work":

  ###### libs/ticket-list-view/src/lib/ticket-details/ticket-details.component.html

  ```html
     <header class="ticket-header"
             (click)="markToWork(ticket.id)"                                                                                                [class.marked]="markedToWork$ | async">
  ```

<br/>

---

The important lesson here is the separation of concerns.

* One process marks the ticket as "to work"
* Another process passively waits for the observable to push an updated list and will update the DOM accordingly.

---

<br/>


5. Finally, let's update the `ticket-list.component.ts` to watch for the `ticketsToWork$` list and update a counter of current tickets 'marked to work'.

  ###### libs/ticket-list-view/src/lib/ticket-list/ticket-list.component.ts

  ```typescript
  export class TicketListComponent implements OnInit {
    // ... other code here
    ticketsToWork$: Observable<number>;

    constructor(
      private store             : Store<TicketsStateModelState>,
      private ticketTimerService: TicketTimerService) { }

     ngOnInit() {
       // ... other existing code.

       const allTicketsToWork$ = this.ticketTimerService.ticketsToWork$;
       this.ticketsToWork$ = allTicketsToWork$.pipe(

         <USE MAP OPERATOR TO EXTRACT NUMBER OF TICKETS IN THE LIST>

       );
     }
  }
```

Now, let's update the `ticket-list.component.html` template to render the current count of tickets marked as 'to-work'.

  ```html
     <div>Tickets to work: {{ ticketsToWork$ | async }}</div>
  ```

<br/>

### Bonus Exercise

Add a way to remove a ticket from the 'marked to work' status list. This will allow the ticket status *to-work* to be toggled ON/OFF.

<br/>

----

<br/>

### Next Lab

Go to Building Blocks of NgRx Lab #1: [Create a Root State for Logs](/building-blocks-of-ngrx/lab-1.md)
