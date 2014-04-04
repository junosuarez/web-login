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

navigation.login() => Promise<Token>
// Token is a string of a cryptographically secure token representing the user's identity
```

## example
```js
navigation.login().then(function (token) {

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
