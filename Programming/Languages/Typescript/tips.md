# Reduce Heartache

## Be Specific
-   Be specific at all times when defining objects types, param types, etc..
-   Especially when working on large projects, the larger the codebase the more likely you'll run into problems down the line if you aren't consistently specific.
-   e.g
```typescript   
// Unspecific
type PayGrade: number

//Specific
type PayGrade = 1 | 2 | 3 | 4 | 5;

//Extremely Specific
const payGrade = {
    low: 1,
    average: 2, 
    good: 3, 
    better: 4,
    best: 5
} as const
type PayGrade = typeof payGrade [keyof typeof payGrade]

//Now that's Robust
```

## Enable Strict Mode
- Typescript allows strict mode, which gives you a harder time when it comes to type checking.
- Turn it one when possible. 
- located in the **tsconfig.json**
- enable strict toggles seven options:
  - **noImplicitAny**
  - **strictNullChecks**
  - **noImplicitThis**
  - **alwaysStrict**
  - **strictBindCallApply**
  - **strictFunctionTypes**
  - **strictPropertyInitialization**

## Apply Type Parameter Constraint to Generics
- when using a generic type parm. Declare the parm with a constraint. 
- It can be constrained by another type or interface
- e.g
```typescript   
type Animal = {
    owner: string;
    function feedPets<T extends Animal>(pets: T[]): void { }
}
```

## Use Type Inference Instead of Explicit Declaration
- use it to simplify code.
- the compiler can figure out typing for simple type expressions, including variables, return types, etc.
- the simpler the better
```typescript   
// Using explicitly typing string is redundant
const x: string = "Zack"
```

- there are exceptions, and cases however where explicit variables can help with readability
- function params are never inferred because they default to any leading into the next sections

## Use Any as little as possible
- just avoid it. It makes things easier
- use unknown, unknown can be set but not used until it is cast to a type





