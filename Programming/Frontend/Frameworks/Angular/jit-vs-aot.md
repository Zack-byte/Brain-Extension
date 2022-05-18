# JIT VS. AOT in Angular
- **Just in Time** vs **Ahead of Time** compilation in Angular

## What is JIT
- Just in time compilation (also dynamic translation or run-time compilation) is a way of executing computer code that involves compilation during execution of a program.
- Code is compiled when it is needed not before runtime.

## How JIT works
- compilers turn high-level code into object code (machine instructions) which would then be linked to an executable.

- A JIT compiler is a feature of the run-time interpreter, that instead of interpreting bytecode every time a method is invoked.

- It compiles the bytecode into machine code instructions of the running machine, and then invoke this object code instead.


## JIT and AOT Comparison
- Jit compilation is the default when you run the **ng build** or **ng serve** CLI commands. This is for development

- For AOT compilation, include the **--aot** option with the **ng build** or **ng serve** command. Another way is using **--prod** which by default production mode is configured in **angular.json** with AOT set to true.


## How AOT Works
- the compiler extracts metadata to interpret the parts of the application that Angular is supposed to manage.
- @Component() and @Input() are decorators explicit metadata specifications
- You can also specify metadata implicitly in the constructor declarations of the decorated classes. 
- The metadata tells Angular how to construct instances of your application classes and interact with them at runtime


## Compilation phases
- There are three phases of AOT compilation
  - **Code Analysis**
  - **Code Generation**
  - **Template Type Checking**

## Metadata Restrictions
- You write metadata in a subset of typescript that must conform to the following general constraints
  - Limit expression syntax to the supported subset of JavaScript
  - Only reference exported symbols after code folding
  - Only call functions supported by the compiler
  - Decorated and data-bound class members must be specific


## Phase 1: Code Analysis
- The compiler does some of the analytic work of the first phase. It emits the .d.ts type definition files with type information that the AOT compiler needs to generate application code. 
- The AOT Collector analyzes the metadata records in the Angular decorators and outputs metadata info in .metadata.json files. one per .d.ts file.

## Phase 2: Code Folding
- The compiler can only resolve references to exported symbols. 
- The collector can evaluate an expression during collection and record the result in the metadata.json, rather than the original expression. 
- Allowing you to make limited use of non-exported symbols withing expressions
- e.g
```typescript
const template = '<div> {{hero.name}}</div>';

@Component({
    selector: 'app-hero',
    template: template
})
export class Hero Component {
    @Input() hero: Hero;
}
```

- The compiler could not refer to the template constant because it isn't exported. The collector however can fold the template constant into the metadata definition by in-lining its contents. like so

```typescript
@Component({
    selector: 'app-hero',
    template: '<div>{{hero.name}}</div>'
})
export class HeroComponent {
    @Input() hero: Hero;
}
```

## Phase 3: Template Type checking




