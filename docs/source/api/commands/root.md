---
title: root
comments: false
---

Get the root element.


# Syntax

```javascript
.root()
.root(options)
```

## Usage

`.root()` should be chained off another cy command.

**{% fa fa-check-circle green %} Valid Usage**

```javascript
cy.get('footer').root()       // Yield root element (document)
cy.get('nav').within(function(nav) {
  cy.get('a').first().root()  // Yield root element (nav)
})
```

## Arguments

**{% fa fa-angle-right %} options** ***(Object)***

Pass in an options object to change the default behavior of `.root()`.

Option | Default | Notes
--- | --- | ---
`log` | `true` | Whether to display command in Command Log

## Yields

`.root()` yields the root element regardless of what was yielded from a previous command.

The root element yielded is `document` by default. However, when calling `.root()` from within the callback function of a {% url `.within()` within %} command, the root element yielded is the yielded subject of the {% url `.within()` within %} command.

## Timeout

`.root()` will continue to look for the root element for the duration of the {% url `defaultCommandTimeout` configuration#Timeouts %}.

# Examples

## Document

**Get the root element**

```javascript
cy.get('aside').root() // yields document
```

## Root in {% url `.within()` within %}

**Get the root element in a `.within()` callback function**

```javascript
cy.get('form').within(function (form) {
  cy.get('input[name="email"]').type('john.doe@email.com')
  cy.get('input[name="password"]').type('password')
  cy.root().submit() // submits the form yielded from 'within'
})
```

# Command Log

**Get root element**

```javascript
cy.root().should('match', 'html')

cy.get('.query-ul').within(function(){
  cy.root().should('have.class', 'query-ul')
})
```

The commands above will display in the command log as:

![Command Log root](/img/api/root/find-root-element-and-assert.png)

When clicking on the `root` command within the command log, the console outputs the following:

![Console Log root](/img/api/root/console-log-root-which-is-usually-the-main-document.png)

# See also

- {% url `cy.get()` get %}
- {% url `.within()` within %}