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

## request for contributions

feedback, issues, and pull requests welcome. **use cases and security review especially welcome**

Come chat about it in IRC in #weblogin on irc.freenode.net
