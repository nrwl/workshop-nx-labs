# Lab: Create a Ticket Timer Observable

## Time: 30 minutes

### Scenario

Now that performance and race-conditions have been addressed, let's explore creating observables and stopping the **observable execution**. We will also explore how an observable can be shared and the impacts of the sharing.

![starttimer](https://user-images.githubusercontent.com/210413/35164280-5fc82abc-fd0f-11e7-97f8-e71ef3618c6c.jpg)

We will create a custom Observable that emits a ticker value.<br/>
And then we will use that observable [in the `TicketTimerService`] as an Observable API.

<br/>

----

<br/>

### Code Instructions


1. Use the Angular CLI to generate a new `TicketTimerService` in the `ticket-list-view` lib.
  > The Angular CLI adds `@Injectable({  providedIn: 'root' })` to the service so the service auto self-registers as a root provider!

##### In `libs/ticket-list-view/src/ticket-timer.service.ts`

1. Create a class field for a `timer$ : Observable<number>` and instantiate a custom observable.
2. In the Observable Execution area, set up a count variable and use `setInterval` to increment it every `1000ms`. Make a call to `observer.next` in the setInterval callback and emit the current counter value.
3. Capture the handle to the `setInterval` and use it when creating a *teardown* function. Teardown functions are needed to clean up producer activity when the observer unsubscribes. In this case, we need to return a function that clears the interval with `clearInterval`).

##### In `ticket-details.component.ts`

4. Inject the service into the `constructor`. When the "Start a Timer" button is clicked, set the `timer$` class field to the `timer$` property in the `TicketTimerService` object .

### Code Snippets

###### `ticket-timer.service.ts`

![rxjs4 1](https://user-images.githubusercontent.com/210413/47622805-5e512480-dad7-11e8-8bbb-31e3e1d8b450.jpg)

###### `ticket-details.component.ts`

![rxjs4 2](https://user-images.githubusercontent.com/210413/47622804-5e512480-dad7-11e8-888b-17173d872de3.jpg)

###### `ticket-details.component.html`

![rxjs4 3](https://user-images.githubusercontent.com/210413/47622803-5e512480-dad7-11e8-9091-defca17547fe.jpg)


### Investigate

Run the application and:

*  Start the timer... see the timer values increment.
*  Route to a different view and return to the `TicketDetailsComponent`, confirm the timer is no longer working.

Questions 
  **1)** Why does the timer stop on routing?
  **2)** What happens when you navigate away from the ticket?
  **3)** Why does the start timer not start immediately after clicking?

Add a `console.log()` in the teardown function of your TicketTimerService. Trying navigating again and watch the console.

<br/>

### Bonus Exercise

*  Set up an array of `Observable<number>` as timers and push the `TicketTimer` service timer into it.
*  Then update the template to `ngFor` the timers and use the async pipe to display each timer value.




<br/>

----

<br/>

### Next Lab

Go to RxJS Lab #5: [Track Tickets to Work With a Multi-Cast Observable](lab-5.md)
