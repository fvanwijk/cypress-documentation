slug: location
excerpt: Get the `window.location`

Get the `window.location`.

Given a remote URL of `http://localhost:8000/app/index.html?q=dan#/users/123/edit`, an object would be returned with the following properties:

Key | Type | Returns
--- | --- | ----
`hash` | string | #/users/123/edit
`host` | string | localhost:8000
`hostname` | string | localhost
`href` | string | http://localhost:8000/app/index.html?q=brian#/users/123/edit
`origin` | string | http://localhost:8000
`pathname` | string | /app.index.html
`port` | string | 8000
`protocol` | string | http:
`search` | string | ?q=brian
`toString` | function | http://localhost:8000/app/index.html?q=brian#/users/123/edit

| | |
|--- | --- |
| **Returns** | location object detailed above |
| **Timeout** | *cannot timeout* |

***

# [cy.location()](#section-usage)

Get the `window.location`

***

# Options

Pass in an options object to change the default behavior of `cy.location`.

**cy.location( *options* )**

Option | Default | Notes
--- | --- | ---
`log` | `true` | whether to display command in command log

***

# Usage

## Assert that a redirect works

```javascript
// we should be redirected to the login page
cy
  .visit("http://localhost:3000/admin")
  .location().its("pathname").should("eq", "/login")
```

***

## Check location for query params and pathname

```javascript
// we can yield the location subject and work with
// it directly as an object
cy
  .get("#search").type("brian{enter}")
  .location().then(function(location){
    expect(location.search).to.eq("?search=brian")
    expect(location.pathname).to.eq("/users")
    expect(location.toString()).to.eq("http://localhost:8000/users?search=brian")
  })
```

***

# Notes

## Do not use `window.location`

Let's examine the following scenario:

```javascript
// get our remote window and log out
// the window.location object
cy.window().then(function(window){
  console.log(window.location)
})
```

```javascript
// go through the location command
// and log out this object
cy.location().then(function(location){
  console.log(location)
})
```

Cypress automatically normalizes the `cy.location()` command and strips out extrenuous values and properties found in `window.location`. Also the object literal returned by `cy.location()` is just a basic object literal, not the special `window.location` object.

When changing properties on the real `window.location` object, it will force the browser to navigate away. In Cypress, the object we returned is a plain object, and changing or affecting its properties will have no effect on navigation.

***

# Command Log

## Assert on the location's href

```javascript
cy.location().its("href").should("include", "#users/new")
```

The commands above will display in the command log as:

<img width="581" alt="screen shot 2015-11-29 at 1 39 13 pm" src="https://cloud.githubusercontent.com/assets/1271364/11459185/b2bca74a-969e-11e5-85b5-3d154efd57a7.png">

When clicking on `location` within the command log, the console outputs the following:

<img width="818" alt="screen shot 2015-11-29 at 1 39 30 pm" src="https://cloud.githubusercontent.com/assets/1271364/11459186/b6766bc8-969e-11e5-85b4-d9a1c67e6ef2.png">

***

# Related

- [hash](https://on.cypress.io/api/hash)
- [url](https://on.cypress.io/api/url)