# Lab: Throttle Assigned to User Field and Transform

## Time: 20 minutes

## Scenario

While searching is working for users and tickets, we have a performance issue!

![lab1_snapshot](https://user-images.githubusercontent.com/210413/35134346-67e08b64-fc9b-11e7-9756-aec2e5e38a7f.jpg)

For each change in the AssignedUsers search criteria, we are thrashing the server:

*  We are not waiting until the user appears to have finished changing the criteria.
*  We are querying the server with possible same query as the most recent, previous query.


Let's fix these **performance issues**!

<br/>

----

<br/>

## Instructions

1. In `search-tickets.component.ts`, use the `pipe` method on the `assignedToUser.valueChanges` observable.

###### libs/ticket-list-view/src/search-tickets/search-tickets.component.ts

  ```typescript
    ngOnInit() {
        this.subscription = this.assignedToUser.valueChanges
          .pipe(
            
          )
          .subscribe(value => { ... });
    }  
  ```
  
  <br/>

2. In `search-tickets.component.ts`, import and use the `debounceTime` and `distinctUntilChanged` operators for the `assignedToUser` observable... to manage and throttle the user lookup queries. A good suggested debounce time is **500** milliseconds, although feel free to try out different values and see what the user experience is like!

  ```typescript
    import { debounceTime, distinctUntilChanged } from 'rxjs/operators';
    
    
    export class SearchTicketsComponent implements OnInit, OnDestroy  {   

        ngOnInit() {
            this.subscription = this.assignedToUser.valueChanges
              .pipe(
                <ADD DEBOUNCETIME AND DISTINCTUNTILCHANGED OPERATORS HERE >
              )
              .subscribe(value => { ... });
        }
        
     }
  ```

  <br/>

3. In `search-tickets.component.ts`, use the `filter` operator on `assignedToUser` to only allow value strings with a length greater than zero.

  ```typescript
    import { debounceTime, distinctUntilChanged, filter } from 'rxjs/operators';
    
    
    export class SearchTicketsComponent implements OnInit, OnDestroy  {   

        ngOnInit() {
            this.subscription = this.assignedToUser.valueChanges
              .pipe(
                <ADD FILTER OPERATOR HERE>
              )
              .subscribe(value => { ... });
        }
        
     }
  ```

  <br/>
  
4. In `search-tickets.component.ts`, use the `tap` operator on `assignedToUser` to set the `users` class field to `null` when the length of `value` is zero.


  ```typescript
    import { debounceTime, distinctUntilChanged, filter, tap } from 'rxjs/operators';
    
    
    export class SearchTicketsComponent implements OnInit, OnDestroy  {   

        ngOnInit() {
            this.subscription = this.assignedToUser.valueChanges
              .pipe(
                <ADD TAP OPERATOR HERE>
              )
              .subscribe(value => { ... });
        }
        
     }
  ```

  <br/>
  
5. In `search-tickets.component.ts`, use `pipe` with the `map` operator on the `UserService.users` observable to transform each user object to just the `fullName` property; this is known as *extracting a property value*. Update the `users` class field to be an array of strings and update the template `ngFor` logic for the suggest on type.

  >  Hint: you can use `Array.map()` within the observable `map` operator.

  ```typescript
    import { debounceTime, distinctUntilChanged, filter, tap } from 'rxjs/operators';
    
    
    export class SearchTicketsComponent implements OnInit, OnDestroy  {   

        ngOnInit() {
            this.subscription = this.assignedToUser.valueChanges
              .pipe(
                ...
              )
              .subscribe(value => { 
                this.userService.users(value)
                  .pipe(
                    <ADD MAP OPERATOR HERE>
                  )
                  .subscribe(userFullNames => { ... });              
              });
        }
        
     }
  ```
  <br/>
  
### Investigate

This ^ code works great to manage and control REST server queries. 

There is, however, a **bad practice** code implementation here.. and an actual super-subtle **race-condition** bug! 

Be prepared to discuss it!  
>  Don't cheat and look ahead! ;-)

<br/>

----

<br/>

## Next Lab

Go to RxJS Lab #3: [Use SwitchMap](lab-3.md)
