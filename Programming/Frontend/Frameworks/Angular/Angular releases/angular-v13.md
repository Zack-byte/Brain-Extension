# Angular 13 release

- Released with an emphasis on Ivy enhancements. (Angular compilation engine).

- "Ivy Everywhere" 


## View Engine
- Angular's legacy compilation Engine is no longer available in Angular as of v13. Removing View Engine also means that Angular can reduce its reliance on ngcc (Angular Compatibility compiler) in the future, and teams can look forward to faster compilation because metadata and summary files are no longer included.

## Angular Package Format (APF)
- has been streamlined and modernized to better serve developers.
- Removed older output formats, including View Engine specific metadata.
- More standardization on JS formats such as ES 2020. 
- APF also supports Node Package Exports now. This will help devs from inadvertently relying on internal API's that may change.


## Component API Updates
- QOL improvements on the way devs can dynamically create components.
- The Api has been simplified to reduce boilerplate code.
- Such as ComponentFactoryResolvers being injected into the constructor every single time.

## Removed IE11 support
- Removing this support allows Angular to leverage modern browser features such as CSS variables and web animations via native web APIs. Also apps will be smaller and load faster because those IE11 polyfills and code paths will be removed.
- Removes the need for differential loading


## Improvements to Angular CLI
- now supports the use of persistent build cache by default for new v13 projects. 
- tooling updates which results in up to 68% improvement in build speed and more ergonomic options. 
- ESBuild also has some performance improvements in this release. 
- esbuild which now works with terser to optimize global scripts. esbuild supports CSS sourcemaps and can optimize global CSS, and stylesheets.


## RxJS 7.4 is now default on ng new projs

## Inlining
- Added support for inlining Adobe Fonts which can improve app performance by speeding up the First Contentful Paint (FCP). 