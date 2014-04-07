web-login
=========

bare-bones browser-based identity for the web

## design goals

- support multiple identity providers / protocols
- universal login api for web platform
- small API surface, simple token
- privacy-preserving, doesn't leak additional user information without their knowledge
- no extra features / protocols / barriers to implementation or adoption

## api

```js

navigator.login() => Promise<Token>
// Token is a string of a cryptographically secure token representing the user's identity
```

## example

See the [demo](http://jden.us/web-login-prollyfill/).

```js
navigator.login().then(function (token) {

  // token = eg 7a14d72ae2c75497c7533e63a6ca2720888b204e

  return http.post({
    location: 'https://example.com/sessions',
    data: {token: token}
  })

})
.catch(function (err) {
  console.log('could not log in:', err)
})
.then(loggedInMain)
```

## sequences

### Normal Login
![](http://g.gravizo.com/g?
  @startuml;
  ;
  actor User;
  participant "Client Side App";
  participant Browser;
  participant "Identity Provider";
  participant Server;
  ;
  User -> "Client Side App": Click login button;
  "Client Side App" -> Browser: call navigator.login%28%29;
  Browser -> User: Ask user to pick IDP;
  User -> Browser: Choose IDP;
  Browser -> "Identity Provider": Initiate authentication process;
  "Identity Provider" -> User: Do user authentication process, if any;
  User -> "Identity Provider": Complete authentication process;
  "Identity Provider" -> Browser: Return IDP token;
  Browser -> "Client Side App": Return hashed WebLogin Token;
  "Client Side App" -> Server: Authenticate with WebLogin Token;
  Server -> "Client Side App": Begin authenticated user session...;
  ;
  @enduml;
)

Depending on the User Agent, users may be able to cache their Identity Provider credentials (for example, a "remember my username and password" checkbox) to eliminate some user-involved steps in this process.

## request for contributions

feedback, issues, and pull requests welcome. **use cases and security review especially welcome**

Come chat about it in IRC in #weblogin on irc.freenode.net
