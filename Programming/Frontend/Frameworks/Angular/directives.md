# Angular Directives
Directives in Angular are'nt incredibly complex. In fact they are meant to be the opposite. Quick, easy, and lightweight solutions to help devs speed up the Markup Process of frontend development.

Simply Put, directives are prebuilt or custom baked "plugins" that can be utilized in your HTML elements to simplify static and dynamic Markup transformations.

## Popular Directives
1. ***ngIf** - dynamically renders the current element on the page depending on the result of the supplied boolean value.
    ```typescript
        /** IN component.ts */
        const showContainer = true;
    ```
    ```html
        <!-- IN component.html-->
        <div *ngIf="showContainer">Show Me</div>
    ```
2. ***ngFor** - Renders the specified element for each item in the supplied array.
   ```typescript
   /** IN component.ts */
   const myArray = [{name: "Sam"}, {name: "Veronica"}];
   ```
   ```html
   <!-- IN component.html -->
   <div *ngFor="let item in myArray">
    {{ item.name }}
    </div>

    <!-- W/ Array Index -->
    <div *ngFor="let item in myArray; index as i">
        Item at {{ i }} Equals {{ item.name }}
    </div>
   ```
3. **[ngClass]** - Adds and removes CSS classes based on supplied values.
 ```typescript
    /** IN component.ts */
    const isContainer = true;
 ``` 
 ```html
 <!-- Boolean Assertions can be utilized for clean inline class switching -->
 <div [ngClass]="isContainer == true ? 'container-class' : 'label-class'">
 </div>

 <!-- As a list -->
<div [ngClass]="['first', 'second']"></div>
 ```

## Custom Directives
- As a professional problem solver I like to know how everything is done and also how to do everything. Throughout my career I've found multiple instances when that itch, could not be scratched. In the case of directives however, the Angular dev team seems to get me. Giving me (and whoever reads this) a way to create our own attribute directives.
- Again Plain and Simple...
    1. run this cmd in the Angular CLI
        ```cmd
            ng generate directive test
        ```
        This will create a file <span style="background-color: grey">src/app/test.directive.ts</span> a test file <span style="background-color: grey">src/app/test.directive.spec.ts</span> and adds the directive to the project **AppModule**
    
    2. **Make Some Magic Happen** - next is were you come in as a dev. In the <span style="background-color: grey">"directive.ts"</span> file flesh out some logic to be applied whenever your directive is **USED** on an HTML element **AND** that element is **Rendered**.
   ```typescript
   import { Directive, ElementRef } from '@angular/core';

   @Directive({
    selector: '[appTest]'
   })
   export class TestDirective {
    constructor(private el: ElementRef) {
        this.el.nativeElement.style.backgroundColor = 'yellow'
    }
   }
   ``` 
   3. **Apply That Magic** - Now just slap that Directive on an Element in your HTML and Bob's your uncle...Possibly.
   ```html
    <span appTest>Test Text</span>
   ```

- **Result**
    <div style="background-color: white; padding: 10px">
        <mark>Test Text</mark>
    </div>

## Utilizing HostListener
Thought about moving on or going to sleep until I saw something quick and interesting, that is utilizing the <span style="background-color: grey">angular/core</span> **@HostListener** import. When you're creating a directive and in need of executing logic after an event is emitted on the source element, @HostListener is there for you. It's super simple and a single example should sum up not only its syntax but also its general usage (I'll come back and revise if I ever find otherwise :wink:).

```typescript
//** Of Course you would import like this. */
import { HostListener } from 'angular/core'

//** Then Implement in your directive like this. */
@Directive({
  selector: '[appHighlight]'
})
export class HighlightDirective {

  constructor(private el: ElementRef) { }

  @HostListener('mouseenter') onMouseEnter() {
    this.highlight('yellow');
  }

  @HostListener('mouseleave') onMouseLeave() {
    this.highlight('');
  }

  private highlight(color: string) {
    this.el.nativeElement.style.backgroundColor = color;
  }

}
```
