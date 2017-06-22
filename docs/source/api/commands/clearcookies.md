---
title: clearCookies
comments: false
---

Clear all browser cookies.

{% note warning %}
Cypress automatically clears all cookies *before* each test to prevent state from being shared across tests. You shouldn't need to use this command unless you're using it to clear a specific cookie inside a single test.
{% endnote %}

# Syntax

```javascript
cy.clearCookies()
cy.clearCookies(options)
```

## Usage

`cy.clearCookies()` cannot be chained off any other cy commands, so should be chained off of `cy` for clarity.

**{% fa fa-check-circle green %} Valid Usage**

```javascript
cy.clearCookies()     // clear all cookies
```

## Arguments

**{% fa fa-angle-right %} options** ***(Object)***

Pass in an options object to change the default behavior of `cy.clearCookies()`.

Option | Default | Notes
--- | --- | ---
`log` | `true` | Whether to display command in Command Log
`timeout` | {% url `responseTimeout` configuration#Timeouts %} | Total time to wait for the `cy.clearCookies()` command to be processed

## Yields

`cy.clearCookies()` yields `null`.

## Timeout

`cy.clearCookies()` will wait up for the duration of {% url `responseTimeout` configuration#Timeouts %} for the automation server to process this command.

# Examples

## Clear Cookies

**Clear all cookies after logging in**

In this example, on first login our server sends us back a session cookie. After invoking `cy.clearCookies()` this clears the session cookie, and upon navigating to an unauthorized page, our server should have redirected us back to login.

```javascript
// assume we just logged in
cy.contains('Login').click()
cy.url().should('include', 'profile')
cy.clearCookies()
cy.visit('/dashboard') // we should be redirected back to login
cy.url().should('include', 'login')
```

# Command Log

**Clear cookies after getting cookies**

```javascript
cy.getCookies().should('have.length', 1)
cy.clearCookies()
cy.getCookies().should('be.empty')
```

The commands above will display in the command log as:

![Command Log](/img/api/clearcookies/clear-all-cookies-in-cypress-tests.png)

When clicking on `clearCookies` within the command log, the console outputs the following:

![Console Log](/img/api/clearcookies/inspect-cleared-cookies-in-console.png)

# See also

- {% url `cy.clearCookie()` clearcookie %}
- {% url 'Cypress Cookies API' cookies %}
- {% url `cy.getCookie()` getcookie %}
- {% url `cy.getCookies()` getcookies %}
- {% url `cy.setCookie()` setcookie %}