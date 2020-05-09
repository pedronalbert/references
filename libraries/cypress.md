# Cypress

## CLI
```
cypress open --project: ./foo
cypress run --project: ./foo
```

## Commands
- [cy.screenshot(filename: String?, options: Object?)](https://docs.cypress.io/es/api/commands/screenshot.html)
- cy.go
- cy.reload
- cy.visit(url: String)

### Selectors
```js
cy.get(selector: String);
cy.contains(text: String);
cy.contains(selector: String, text: String);
```

### Custom Commands
```js
Cypress.Commands.add(name: String, (...args) => {
  // logic...
});

// Usage
cy.commandName(...props);
```

## Actions
```js
.click()
.dblclick()
.type()
.clear()
.check()
.uncheck()
.select(item)
```


## Aliasing
We can set alias in our selections
```js
cy.get('#button').as('fooButton');

// Usage
cy.get('@fooButton');
```

## Fixtures
```js
cy.fixture(filepath: String).as(fooData);

cy.get('@fooData').then((fooData) => {

});
```
