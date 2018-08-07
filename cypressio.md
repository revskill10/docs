# Cypress.io

In-browser (with capability to run headless in CI environments) end-to-end testing platform.

Made from two parts: Test runner (required - free) and dashboard service (optional - for nice overview and reports - paid)

## Requirements

1. have Cypress [installed](https://docs.cypress.io/guides/getting-started/installing-cypress.html#npm-install)
2. have [opened](https://docs.cypress.io/guides/getting-started/installing-cypress.html#Opening-Cypress) test runner in order to generate project test structure

## [Test runner](https://docs.cypress.io/guides/core-concepts/test-runner.html)

Interactive (in headed mode) runner with test commands list, live app preview and test selector playground.

## [Dashboard service](https://docs.cypress.io/guides/core-concepts/dashboard-service.html)

Web service allowing to overview passed, failed and running test with video, screenshots and performance reports.

## Directory structure

Cypress creates following directory structure by default

```
|- cypress
  |- fixtures # mocking data
  |- integration # test specs
  |- plugins # Cypress plugins configuration
  |- support # Cypress runner overrides and custom commands
```

and configuration file `cypress.json`.

Structure can be [altered](https://docs.cypress.io/guides/references/configuration.html#Folders-Files) when necessary, but good practice is to keep it.

## Bundled tools

Cypress uses [Mocha](http://mochajs.org) **BDD** style with [Chai](http://chaijs.com) assertions and [Sinon](http://sinonjs.org) library for [stubbing](https://docs.cypress.io/api/commands/stub.html#Syntax) and [spying](https://docs.cypress.io/api/commands/spy.html#Syntax) of methods.
These are [bundled](https://docs.cypress.io/guides/references/bundled-tools.html) and no configuration is required.

Other libraries such as [moment.js](http://momentjs.com), [lodash](https://lodash.com) and others are also automatically [included](https://docs.cypress.io/guides/references/bundled-tools.html#Other-Library-Utilities).

## Writing tests

Test specifications are located in `cypress/integration` directory by default. 
Test runner loads all files from here when used with `cypress run` command.

`ES2015` syntax is supported by default.

### Test cases should

- be descriptive as much as possible
- be simple to read and maintain
- be divided into logical, atomic parts
- utilize hooks for shared commands
- prepare required app state in `before` hooks

### Test cases should NOT

- depend on other cases
- cover more than one specific area
- use `cy.wait` command 

#### Example

> Taken from official [documentation](https://docs.cypress.io/guides/references/best-practices.html#2-Run-shared-code-before-each-test)

```javascript
describe('my form', () => {
  beforeEach(() => {
    cy.visit('/users/new')
    cy.get('#first').type('Johnny')
    cy.get('#last').type('Appleseed')
  })

  it('displays form validation', () => {
    cy.get('#first').clear() // clear out first name
    cy.get('form').submit()
    cy.get('#errors').should('contain', 'First name is required')
  })

  it('can submit a valid form', () => {
    cy.get('form').submit()
  })
})
```

## Running tests

Simplest way to run tests is do add custom command to `package.json` file

```json
{
  "scripts": {
    "cy:run": "cypress run"
  }
}
```

and then use `npm run cy:run` or `yarn cy:run` from command line or CI configuration.

## General DO's and DON'Ts

### DO's

- use `cy.get([data-test="SELECTOR"])` for selectors as these are most insulated from changes
- use aliases for repeated selectors

  ```javascript
  // alias all of the tr's found in the table as 'rows'
  cy.get('table').find('tr').as('rows')
  
  // and then use them is selector
  cy.get('@rows').first().click()
  ```
  
- [stub](https://docs.cypress.io/guides/guides/network-requests.html#Stubbing) API calls when "live" version is not necessary

### DON'Ts

- use generic selectors like `cy.get('.row')`, `cy.get('[name="FORM_INPUT_NAME"]')` as these can be changed in development process
- overuse `cy.wait` as most Cypress commands has meaningful timeouts themselves 

### Tips

### For not repeating same [data-test=] parts
 
To keep test specs DRY and not repeat "long" selector parts, you can use this command override.
Just put this snippet to your `cypress/support/commands.js` file in order to override Cypress `cy.get`.

```javascript
Cypress.Commands.overwrite('get', (originalFn, selector, options) => {
  if (!selector.includes('data-test') && !selector.includes('[')) {
    selector = `[data-test="${selector}"]`
  }
  return originalFn(selector, options)
})
```
