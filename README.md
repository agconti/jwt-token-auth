# JWT token auth for express.js
[![NPM](https://nodei.co/npm/jwt-token-auth.png?compact=true)](https://npmjs.org/package/jwt-token-auth?compact=true)
[![Build Status](https://travis-ci.org/agconti/jwt-token-auth.svg?branch=master)](https://travis-ci.org/agconti/jwt-token-auth)

This package provides [JSON Web Token Authentication](http://tools.ietf.org/html/draft-ietf-oauth-json-web-token) support for
[Express](http://expressjs.com/).

New to using JSON Web Tokens? Take a look at these resources:

- [JSON Web Token Abstract](http://self-issued.info/docs/draft-ietf-oauth-json-web-token.html)
- [Token based authentication with Socket.io](https://auth0.com/blog/2014/01/15/auth-with-socket-io/)
- [JWT.io](http://jwt.io/)

# Installation 
```bash
npm install jwt-token-auth
```

# Usage
```js
var express = require('express')
  , auth = require('jwt-token-auth')
  , app = express()


// Require jwt authorization on all routes
app.use(auth.jwtAuthProtected)

// Reguire jwt auth on a specfic route
app.get('/', auth.jwtAuthProtected, function(req, res){
  res.send({'msg': 'Im jwt auth protected!'})
})

app.listen(3000)
```
Now your route(s) are protected and require an authorization header in the form of:

```
Authorization JWT < jwt token > 
```

# Configuration
Configure your JWT Secret. This must be changed for production. Default value is `'secret'`. 
```js
process.env.JWT_SECRET_KEY = 'Your Secret'
```

Configure the authorization header prefix. this is optional. Default is `'JWT'`.
```js
process.env.jwtAuthHeaderPrefix
```

# Provided Middleware

## ensureAuthorizationHeader
An Express.js middleware that ensures that a request has supplied an authorization header.
* @param {object} req
* @param {object} res
* @param {function} next

## validateJWTAuth
An Express.js middleware validates a JWT token.
 * @param {object} req
 * @param {object} res
 * @param {function} next

## ensureAuthorized 
An Express.js middleware that ensures that a request has supplied an authorization header.
* @param {object} req
* @param {object} res
* @param {function} next

## jwtAuthProtected 
The grouped middleware needed to enforce jwt Auth. Mounts the same as a single middleware.

# Errors 
When authorization fails jwt-token-auth will return an `UnauthorizedError` with some helpful details about what went wrong. 
 
This implementation was based on the excellent [django-rest-framework-jwt library](https://github.com/GetBlimp/django-rest-framework-jwt).
