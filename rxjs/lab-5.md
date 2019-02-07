# RxJS Lab 5: Use BehaviorSubject

## Time: 20 minutes

## Scenario

In this last, we will use the concepts of UniCast and MultiCast observables and explore a solution using a `BehaviorSubject` .

![startwork](https://user-images.githubusercontent.com/210413/35168754-c42e14b6-fd1f-11e7-93e8-af0836b3ff3c.jpg)

Using a **BehaviorSubject** to cache the current list of tickets with "work" status is useful for future subscribers... as they will then get the updated, current list.


## Instructions

##### In `ticket-timer.service.ts`, 

1. Create a private class field for cache a list of 'working' ticket ids.
2. Add a private class field for tickets to work.
3. Instantiate to a new `BehaviorSubject` with an initial value of the current empty `_ticketsIdsToWork` list.
4. Create a accessor (aka getter) field to publish the private tickets-to-work list.
5. Create an `addTicketIdToWork()` class method to add ticket id to the internal, private list and then use the *BehaviourSubject* `next()` to announce the changes to external observers.
  > Note: you should announce the changes using a clone of the list. **Question:** Why?

##### In `ticket-details.component.ts`, 

1. This view component has a click handler on the header to call `markToWork()`. Update `markToWork()` to make a call to the ticket timer service method to add a ticket id to work.
2. In (3) above we added code to add a ticket to our 'to-work' list. Now we need to configure (using observables) a watch to update the header color when the current ticket is contained in the 'work in-progress' list.

##### In `ticket-details.component.html`, 

Use class data binding to update CSS header stylings when the current ticket is "marked to work":

##### In `ticket-list.component.ts` 

Watch for the `markedToWork$` list and update a counter of current tickets 'marked to work'.

##### In `ticket-list.component.html ` 

Now, let's update template to render the current count of tickets marked as 'to-work'.


<br/>

---

The important lesson here is the separation of concerns.

* One process marks the ticket as "to work"
* Another process passively waits for the observable to push an updated list and will update the DOM accordingly.

---

### Code Snippets

###### `ticket-timer.service.ts`

![ticket-timer.service.ts](https://user-images.githubusercontent.com/210413/47942022-81584b80-debe-11e8-872b-3c476a0d99e7.png)

###### `ticket-details.component.ts`

![ticket-details.component.ts](https://user-images.githubusercontent.com/210413/47942039-903efe00-debe-11e8-84aa-e20bd46c8d96.png)

###### `ticket-details.component.html`

![ticket-details.component.html](https://user-images.githubusercontent.com/210413/47942058-9fbe4700-debe-11e8-92cb-5cafd2011adf.png)

###### `ticket-list.component.ts`

![ticket-list.component.ts](https://user-images.githubusercontent.com/210413/47942074-af3d9000-debe-11e8-84b6-09f1f963388e.png)

###### `ticket-list.component.html`

![ticket-list.component.html](https://user-images.githubusercontent.com/210413/47942090-bcf31580-debe-11e8-8a2f-c0980fb40f34.png)

<br/>

### Bonus Exercise

Add a way to remove a ticket from the 'marked to work' status list. This will allow the ticket status *to-work* to be toggled ON/OFF.


<br/>

----

<br/>

### Next Lab

Go to RxJS Lab #6: [Combining Observables](/rxjs/lab-6.md)
