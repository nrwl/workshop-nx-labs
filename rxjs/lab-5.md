# Lab 5: Use BehaviorSubject

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
2. In (3) above we added code to add a ticket to our 'to-work' list. Now we need to configure (using observables) a watch to update the header color when the current ticket is in that 'to-work' list.

##### In `ticket-details.component.html`, 

Use class data binding to update CSS header stylings when the ticket is "marked to work":

##### In `ticket-list.component.ts` 

Watch for the `ticketsToWork$` list and update a counter of current tickets 'marked to work'.

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

![rxjs5 1](https://user-images.githubusercontent.com/210413/47623212-8abb6f80-dadc-11e8-895c-09a176387a29.jpg)
###### `ticket-details.component.ts`

![rxjs5 2](https://user-images.githubusercontent.com/210413/47623211-8abb6f80-dadc-11e8-97b4-04d40c44348e.jpg)

###### `ticket-details.component.html`

![rxjs5 3](https://user-images.githubusercontent.com/210413/47623210-8abb6f80-dadc-11e8-8f36-9af7dea2ee9c.jpg)

###### `ticket-list.component.ts`

![rxjs5 4](https://user-images.githubusercontent.com/210413/47623209-8abb6f80-dadc-11e8-910e-b0ede49de17b.jpg)

###### `ticket-list.component.html`

![rxjs5 5](https://user-images.githubusercontent.com/210413/47623208-8abb6f80-dadc-11e8-96be-fcb974fa7f6a.jpg)

<br/>

### Bonus Exercise

Add a way to remove a ticket from the 'marked to work' status list. This will allow the ticket status *to-work* to be toggled ON/OFF.


<br/>

----

<br/>

### Next Lab

Go to Building Blocks of NgRx Lab #1: [Create a Root State for Logs](/building-blocks-of-ngrx/lab-1.md)
