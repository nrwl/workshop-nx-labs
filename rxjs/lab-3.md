# Lab: Use SwitchMap

## Time: 20 minutes

## Scenario

In the last lab, we fixed the server-thrashing performance issue(s)! 

<br/>

![lab1_snapshot](https://user-images.githubusercontent.com/210413/35134346-67e08b64-fc9b-11e7-9756-aec2e5e38a7f.jpg)

But **now** we have some subtle race-conditions to fix!  The server may respond with out-of-order responses to the AssignedUser query. What we need to do is cancel the previous query/search before we issue another new query to the server!

Let's fix these **race-condition issues**!

<br/>

----

## Instructions
1. In `search-tickets.component.ts`, refactor the `assignedToUser.valueChanges` pipe of operators to remove the `tap` operator.

2. In `search-tickets.component.ts`, use the `switchMap` operator in the `assignedToUser.valueChanges` pipe and return the call to `UserService.users` from that. Make sure it still has the `map` operator for it!

  ###### libs/ticket-list-view/src/search-tickets/search-tickets.component.ts

  ```typescript
    import { debounceTime, distinctUntilChanged, filter, switchMap } from 'rxjs/operators';
    
    
    export class SearchTicketsComponent implements OnInit, OnDestroy  {   

        ngOnInit() {
            this.subscription = this.assignedToUser.valueChanges
              .pipe(
                <ADD SWITCHMAP OPERATOR HERE>
              )
              .subscribe(value => { ... });
        }
        
     }
  ```

  <br/>


2. In `search-tickets.component.ts`, change the `users` class field to be an observable


  ```typescript
    import { debounceTime, distinctUntilChanged, filter, switchMap } from 'rxjs/operators';
    
    
    export class SearchTicketsComponent implements OnInit, OnDestroy  {   
        users$ : Observable<string[]>;
        
        ngOnInit() {
          ...
        }
        
     }
  ```
  
  >  Note the use of the `$` suffix in `users$`. This is a recommended notation standard for all observable variables. Also note that this is an observable of a **string[]**. Why is that ?

  <br/>  
  
3. In `search-tickets.component.ts`, remove the `subscribe` to the `valueChanges` that contained the `UserService` call.


  ```typescript
    import { debounceTime, distinctUntilChanged, filter, switchMap } from 'rxjs/operators';
    
    
    export class SearchTicketsComponent implements OnInit, OnDestroy  {   

        ngOnInit() {
            this.users$ = this.assignedToUser.valueChanges.pipe(
                ....                
            );
        }
        
     }
  ```
  
  >  Note: 

  <br/>     
     
4. In `search-tickets.component.ts`, get rid of the `subscription` class field and the call to `unsubscribe()` in `ngOnDestroy`.

  <br/>   
  
5. In `search-tickets.component.html`, update the template to use the `async` pipe for the users.

 ```html
    <li *ngFor="let userFullName of (users$ | async)" (click)="setAssignedToUser(userFullName)">
      {{userFullName}}
    </li>
  ```  

  <br/>   

----

<br/>

### Bonus Exercise

When the AssignedUsers search criteria field is empty, how can you auto-clear the dropDown menu?

> Please do NOT use the `tap()` operator. Hint use `Observable.of()`

<br/>

----

<br/>

### Next Lab

Go to RxJS Lab #4: [Create a Ticket Timer Observable](lab-4.md)
