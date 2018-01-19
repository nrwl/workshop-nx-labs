# Lab: Create a Ticket Timer Observable

## Scenario

Now that performance and race-conditions have been addressed, let's explore creating observables and stopping the **observable execution**. We will also explore how an observable can be shared and the impacts of the sharing.

![starttimer](https://user-images.githubusercontent.com/210413/35164280-5fc82abc-fd0f-11e7-97f8-e71ef3618c6c.jpg)

We will create a custom Observable that emits a ticker value and publish that in TimerService that uses Observable API.

<br/>

----

<br/>

## Code Instructions

1. Use the Angular CLI to generate a new `TicketTimer` service in the `ticket-list-view` lib.
  

  ```console
    ng g s ticketTimer --module TicketListView
  ```

   >  Make sure you add it to the providers for the ticket list view module by using the `--module` flag. Open this module to see how the service has been registered.

<br/>

2. In the `ticket-timer.service.ts`, create a class field for a `timer$ : Observable<number>` and instantiate a custom observable.

  ```js
    private timer$ = Observable.create(observer => {
      // Add the observable Exection HERE... aka Producer activity
      
      <OBSERVABLE EXECUTION>
      
      // Tear down function
      return () => {
        
      };
  });
  ```
 
  >  Note: do not just copy this... type it yourself to learn better.
  
  <br/>

3. In the Observable Execution area, set up a count variable and use `setInterval` to increment it every `1000ms`. Make a call to `observer.next` in the setInterval callback and send that the counter value.

  ```js
    private timer$ = Observable.create(observer => {
      
      <OBSERVABLE EXECUTION>
      
      return () => { 
        // ....
      };
  });
  ```
 
  >  Note: do not just copy this... type it yourself to learn better.
  
  <br/>
  
4. Capture the handle to the `setInterval` and use it in teardown logic to clean it up (have the function literal return a function that clears the interval with `clearInterval`).

  ```js
    private timer$ = Observable.create(observer => {      
       // ...
      
      return () => { 
        <ADD  TEARDOWN LOGIC HERE>
      };
  });
  ```
   
  <br/>
  

5. Inject the service into the `TicketDetailsComponent` and set the `timer$` class field to the getter class field from `TicketTimer` service when the "Start a Timer" button is clicked.

  ```js
    export class TicketDetailsComponent implements OnInit {
        timer$ : Observable<number>;

        constructor(
          private store              : Store<TicketsStateModelState>,
          private route              : ActivatedRoute,
          private ticketTimerService : TicketTimerService
        ) {};
        
        startTimer() {
          <USE TICKET TIMER SERVICE HERE>
          
          this.timer$ = ...
        }

    }    
  ```
   
   >  Note: do not just copy this... add the parts needed by typing it yourself.
   
  <br/>

### Investigate

Run the application and:

*  Start the timer... see the timer values increment. 
*  Route to a different view and return tot the `TicketDetailsComponent`, confirm the timer is no longer working.

Why does the timer stop on routing?

Add a `console.log()` in the teardown function of your TicketTimerService. 

Trying navigating again and watch the console.

br/>

### Bonus Exercise

*  Set up an array of `Observable<number>` as timers and push the `TicketTimer` service timer into it. 
*  Then update the template to `ngFor` the timers and use the async pipe to display each timer value. 

Question: What is this doing? 

Question: What happens when you navigate away from the ticket?


<br/>

----

<br/>

### Next Lab

Go to RxJS Lab #5: [Track Tickets to Work With a Multi-Cast Observable](lab-5.md)
