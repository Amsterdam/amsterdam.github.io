---
abstract: OAuth 2.0 authorization service written in Go
---

# Authz

An implementation of the [OAuth 2.0 implicit authorization flow (RFC6749)](https://tools.ietf.org/html/rfc6749#section-1.3.2) as a HTTP service written in Go.

This service:
* creates signed JSON Web Token (JWS) access tokens to be used what RFC6749 calls resource servers
* Can use in-memory state storage or be connected to external storage such as Redis

For more information on how to use, check out the [GitHub repository: Amsterdam/authz](https://github.com/Amsterdam/authz) or the [Documentation on GoDoc](https://godoc.org/github.com/Amsterdam/authz/oauth2).

## Admin backend

Alongside the Authz service we created an [Admin backend (GitHub repository: Amsterdam/authz_admin)](https://github.com/Amsterdam/authz_admin) to map OAuth 2.0 scopes to profiles that map to roles provided by your Identity Provider.