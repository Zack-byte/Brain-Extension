## Why Use Typescript
   - In short, to prevent certain glitches and behaviors that can occur when types are not inforced
   - Quick e.g. in Javascript doing something like below will result in "22" instead of the possibly expected "4"

   ```javascript  
   // userInput = "2"
   console.log(userInput + 2);
   ```
## Static Typing
   - The compiler enforces that values use the same type.

## Why use static typing
   - Most of the time static typing is for performance reasons.
   - There's a benefit to letting the compiler know what type the value is, without having to check it.

## Interfaces
   - You can enforce that a class has certain functions (or props). 
   - "Binding the class with a contract basically"

## Literal Types
   - Is a more concrete sub-type of a collective type. "Subsumption"
   - Available for string, number, or boolean

```typescript  
type Messages = "Written" | "Emailed" | "Word of Mouth"

public recordMessage(name: string, messageType: Messages): void {
   console.log(messageType)
   console.log(name);
}
```

  
   ### Literal Narrowing
   - Letting the compiler know whether or not a variable will change its contents.
   - e.g **var** and **let** won't change and **const** will change


## Cons of Typescript
   - Not supported by Node.js or browsers meaning it has to be compiled to javascript first
   - 