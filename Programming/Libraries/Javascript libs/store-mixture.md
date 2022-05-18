# NGRX, Flux, Redux Mixture

Redux: Javascript library which first originated "stores" it is commonly used in React and angular

Flux: is the application architecture that facebook uses for building client side web applications

A store architecture is recommended if you have a piece of data that needs to be used in multiple places in your app and passing it via props makes your components break the single responsibility principle 

OR

There are multiple independent actors generally the server and the end user that may mutate that data

When to use Redux Stores: 
	- 


Virtual Dom is a programming concept where an ideal or "virtual" representation fo a UI is kept in memory and synced with the "real" DOM by a library such as ReactDOM

	- "Virtual Dom" is more of a pattern then a specific technology



A store is a immutable object tree in Redux: 
	- it is a state container which holds the applications state 
	- redux can have only a single store in your application
	- whenever a store is created in redux you need to specify the reducer.



Redux also solves the "Extraneous(irrelevant) Props" issue 
	- In angular terms Props are the equivalent of the @Input() member variables of an angular component 

The situation is when a store shines: 
	- a store is an ideal solution for this problem of editable data and multiple actors but let's imagine that the data is not being pushed from the server


Stores are a compound solution for multiple problems not just one. 
	- they solve the problem of component interaction via the observable pattern 
	- they provide a client side cache if needed to avoid doing repeated Ajax requests 
	- they provide a place to put temporary UI state as we fill in a large for or want to store search criteria in a search from when navigating between router views
	- and they solve the problem of allowing modification of client side transient data by multiple actors


AJAX is a developers dream because you can: 
	- update a web page without reloading the page
	- request data form a server after the page has loaded 
	- receive data from a server after the page has loaded
	- send data to a server in the background


@ngrx/effects: 
	- Effects are an RxJS powered side effect model for store. Effects use streams to provide new sources of actions to reduce state based on external interactions such as network requests web socket messages and time based events
	- Effects are whee you handle tasks such as fetching data long running tasks that produce multiple events and other external interactions where your components don't need explicit knowledge of these interactions

@ngrx/store: 
	- Store is RxJS powered global state management for angular applications inspired by redux. Store is a controlled state container designed to help write performant consistent applications on top of angular

	- Key Concepts: 
		- Actions describe unique events that are dispatched from components and services. 
		- state changes are handled by pure functions called reducers that take the current state and the latest action to compute a new state. 
		- selectors are pure functions used to select derive and compose pieces of state 
		- state is accessed with the store an observable of state and an observer of actions