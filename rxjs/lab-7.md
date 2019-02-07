# RxJS Lab 7: RxJS + Facades

## Scenario

In this last lab, we will use the concepts of Facades to simplify our view layer and enable super-easy, non-UI component testing.

----

This is a optional **Bonus Lab** based on time and developer interest

----


## Instructions

##### In `libs/ticket-list-view/src/lib/search-facade.ts`, 

1. Create the interfaces that will be used in the `SearchFacade`. 
2. Create the `SearchFacade` with the api and code shown below. 
  > Note: the public API should be observables or methods that return observables!

##### In `search-tickets.component.ts`, 

1. Update the code to inject and use the SearchFacade.
> Be prepared to talk about why the ngOnInit() is needed. 
> Also explain why the SearchFacade does not need to be registered in the `ticket-list-view.module.ts`
 
---

### Code Snippets

###### Interfaces for `search-facade.ts`

![interfaces](https://user-images.githubusercontent.com/210413/52440919-edada100-2ae4-11e9-9c6b-1faf6f81f861.png)

###### `search-facade.ts`

![searchFacade](https://user-images.githubusercontent.com/210413/52440918-edada100-2ae4-11e9-8e83-d19f0ece487b.jpg)

###### `search-tickets.component.ts`

![seach-tickets.component.ts](https://user-images.githubusercontent.com/210413/52440917-ed150a80-2ae4-11e9-9e56-5cefafaea097.png)

<br/>

----

### Bonus

Read the blog article [Angular: You may not need NgRx!](https://blog.angularindepth.com/angular-you-may-not-need-ngrx-e80546cc56ee)


----

<br/>

### Next Lab

Go to NgRx Lab #1: [Actions, Reducers, and Selectors](/ngrx/lab-1.md)
