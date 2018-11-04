# NgRx Lab 2: Composed Store Selectors

![image](https://user-images.githubusercontent.com/210413/47935906-02f1ae80-deaa-11e8-8cd7-0615e6234c76.png)

### Scenario

We need to convert our raw selectors to composed, memoized Store selectors using `createFeatureSelector()` and `createSelector()`

<br/>

### Code Instructions

<br/>

----
    
##### In `tickets.selectors.ts`

1. Import and use the `createFeatureSelector()` to create a `getTicketsState` selector.
2. Use `createSelector` to convert are the other raw selectors to composed, memoized selectors.
  
<br/>


### Code Snippets

###### `tickets.selectors.ts`

![image](https://user-images.githubusercontent.com/210413/47958976-85ab6400-dfa5-11e8-8b47-7dd35c0c32b3.png)


<br/>

----


<br/>

### Investigate

Be prepared to discuss what memoization means for NgRx state and view templates. 


<br/>

### Running the Application

*  Open the **Customer Portal** application with the browser: http://localhost:4203
*  Confirm the **Node Server** is running with browser page:  http://localhost:3000/api/tickets

Run the following command(s) in individual terminals:

```console
yarn server
```

```console
yarn customer-portal -- -o
```

> If you already have one(s) running and need to restart, you can stop the run with `ctrl+c`.


<br/>

----

<br/>

### Next Lab

Go to NgRx Lab #3: [Effects and ReduxTools](lab-3.md)
