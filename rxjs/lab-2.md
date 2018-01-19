# Lab: Throttle Assigned to User Field and Transform

## Scenario

While searching is working for users and tickets, we have a performance issue!

![lab1_snapshot](https://user-images.githubusercontent.com/210413/35134346-67e08b64-fc9b-11e7-9756-aec2e5e38a7f.jpg)

For each change in the AssignedUsers search criter, we are thrashing the server:

*  We are not waiting until the user appears to have finished changing the criteria.
*  We are querying the server with possible same query as the most recent, previous query.


Let's fix these **performance issues**!

<br/>

----

<br/>

## Instructions

1. Use the `pipe` method on the `assignedToUser.valueChanges` observable.

  ```js
    ngOnInit() {
        this.subscription = this.assignedToUser.valueChanges
          .pipe(
            
          )
          .subscribe(value => { ... });
    }  
  ```
  
  <br/>

2. Import and use the `debounceTime` and `distinctUntilChanged` operators for the `assignedToUser` observable... to manage and throttle the user lookup queries.

  ```js
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

3. Use the `filter` operator on `assignedToUser` to only allow value strings with a length greater than zero.

  ```js
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
  
4. Use the `tap` operator on `assignedToUser` to set the `users` class field to `null` when the length of `value` is zero.


  ```js
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
  
5. Use `pipe` with the `map` operator on the `UserService.users` observable to transform each user object to just the `fullName` property (Hint: you will need to do an array `map` within the `map` operator). Update the `users` class field to be an array of strings and update the template `ngFor` logic for the suggest on type.


  ```js
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

This code works great to manage and control REST server qeuries. There is a **bad practice** implementation here. Be prepared to discuss it!  (do not cheat and look ahead!)

<br/>

----

<br/>
## Next Lab

Go to RxJS Lab #3: [Use SwitchMap](lab-3.md)
