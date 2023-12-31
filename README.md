# undici-oauth-interceptor

Manages an access token and automatically sets the `Authorization` header on any
request that is going to a limited set of domains.

## Install

```bash
npm i undici undici-oauth-interceptor
```

## Usage

```javascript
const { Agent } = require('undici')
const { createOAuthIntercpetor } = require('undici-oauth-interceptor')
const dispatcher = new Agent({
  intercpetors: {
    Pool: [createOAuthIntercpetor({
      // Provide a refresh token so the interceptor can manage the access token
      // The refresh token must include an issuer (`iss`)
      refreshToken: '',

      // Set an array of status codes that the interceptor should refresh and
      // retry the request on
      retryOnStatusCodes: [401],

      // The origins that this interceptor will add the `Authorization` header
      // automatically
      origins: []

      // OPTIONAL: an initial access token
      accessToken: ''

      // OPTIONAL: clientId that matches refresh token
      // Default: the `sub` claim in the refresh token
      clientId: null
    })]
  }
})
``` 

## License

MIT
