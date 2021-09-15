# wiki-test

I've used Vue CLI to make this prototype

To install the project run the following commands at the root of the project :
```
npm install
```
then :
```
npm run serve
```
and go to http://localhost:8080/ to browse the app

### Things I would've added if given more time

- accessibility ARIA tags
- better error management
- pagination
- localisation for several languages
- better support for mobile
- "Ghost elements" while the items are loading, to give the impression that the loading is faster

I would also argue that the search bar should be at the top of the page, not at the bottom. When entering a query, the search bar disappears from the viewport.
To avoid this, I chose to make it sticky at the bottom