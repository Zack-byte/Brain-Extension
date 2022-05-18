# Lighthouse (Google)
- is an open-source, automated tool for improving the quality of web pages.
- It provides audits for:
  - performance
  - accessibility
  - progressive web apps
  - SEO
  - etc...

## Running Lighthouse
- You can run it in DevTools, from the command line, or as a Node Module.
- Give it a URL to audit, and you're good to go.
- It will generate a report on how well the page did. 
- Of course form there, use the indicators to evaluate and break down possible problems and solutions for improving your application in said areas.


    ### Running From Dev Tools
    - Of course open DevTools/Audits
    - "Perform an Audit"
    - "Run Audit"
    - And there you go... Pretty straight forward

    ### Running From Node
    - npm install -g lighthouse
    - run "lighthouse (url)"
    - to see all options use "lighthouse -help"

## Lighthouse is Extensible
- can write extensions etc... for lighthouse
### Stack Packs
  - allows lighthouse to detect what platform your site is built on and display specific stack-based recommendations. 

### Plugins
- Allows domain experts in the community to extend the functionality of Lighthouse for their specific needs. you can leverage the data that lighthouse collects to create new audits. 