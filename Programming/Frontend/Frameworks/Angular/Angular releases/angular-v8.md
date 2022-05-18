# Angular 8 release notes
- legacy release however some important pieces in here related to the CLI and Ivy

## Differential Loading of Modern Javascript
- CLI will begin producing both legacy (ES5) and modern (ES2015+) bundles as a part of the build process, which will be differentially loaded client-side to improve the loading speed and time to interactive for modern browsers. 


## What will Ivy look like
- opt-in preview of Ivy. 
- Allow you to switch between the Ivy and View Engine build and rendering pipelines in your project.
- Application will be built with the Ivy compiler and any dependencies you use from Angular or other 3rd parties should keep working as we'll run them through our ngcc.
  - Should see some faster re-build times
  - improved template type checking
  - backwards compatibility
  - easier to read and debug code at runtime
  - improved payload size
  - 