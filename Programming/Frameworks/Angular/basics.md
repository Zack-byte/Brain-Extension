# Angular (JS)(TS)

----------------- Building a Site with Angular 
- You build Angular applications with components
	- they define areas of responsibility in the UI that let you reuse sets of UI functionality 

- Components consist of three things 
	- A component class that handles data and functionality
	- an HTML template that determines the UI
	- Component-specific styles that define the look and feel 

- in the Typescript file after creating a new component the key features consist of 
	- the selector, app-product-alerts, identifies the component. normally naming follows the convention of starting with app for example app-product-alerts 
	- the template and style filenames reference the component's HTML and CSS
	- the @Component() definition also exports the class ProductAlertsComponent which handles functionality for the component. 
	

- Using | inside a data call is called a Pipe...a Pipe is a way to transform data in an HTML template 

- in angular a service is an instance of a class that you can make available to any part of your application using Angular's dependency injection system 

- When running local using angular CLI...it utilizes a tool called webpack that initiates HMR (Hot Module Reloading)

- Angular apps are built on the building blocks called components
	- these components are built on three things
		- Data 
		- HTML Template
		- Logic


- module is a container for a group of related components every application has at least one module but as it grows you can add more and more components 

- the larger your application gets the more modules you want to use in order to de-couple your module 

-------------- TypeScript
- superset of javascript
- Strong Typing
- object-oriented features
- compile-time errors
- great tooling 


- browsers don't understand typescript so we need to transpile our TS code into java script 

- in typescript using a for loop inside a method any variable that is declared in the constructor can also be called and used outside of the for loop as long as it's in the method....
	- to prevent this use the keyword **let** which will apply the same rules such as in c# 

- variables can have

------------ Java Script
- versions; 
	- ES5(ECMAScript 5): supported by all browsers
	- ES6(2015) 
	- ES2016
	- ES2017 


-------------------- SCSS (Syntactically Awesome Stylesheets) 
is a CSS pre-processor that lets you use variables, mathematical operations, mixins, loops, functions, imports, and other interesting functionalities that make writing CSS much more powerful. 

- one of the great benefits of using SASS is the ability to use variables. you can store and reuse values

-  improved syntax
	- allows you to use a nested syntax, which is code contained within another piece of code that performs a wider function. 
	- nesting allows a cleaner way of targeting elements
	- you can nest your HTML elements by using CSS selectors 
		- benefits: 
		- more natural syntax and easy to read in more cases
		- prevents the need to rewrite selectors 
		- multiple times 
		- better code organization and structure thanks to its visual hierarchy 
		- more maintainable code

- Mixins
	- are like functions in other languages
	- they return a value or set of values and can take parameters including default values
	- SASS has functions too (but a mixin is not like a function) 