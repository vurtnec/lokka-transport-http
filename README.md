# @aaxis/lokka-transport-http

Isomorphic HTTP Transport Layer with Expose handle Request and Response 

---

This is a compatible transport layer for [Lokka](https://github.com/kadirahq/lokka).

## Basic Usage

Install the package:

```
npm i --save @aaxis/lokka-transport-http
npm i --save lokka
```

```js
import HttpTransport from '@aaxis/lokka-transport-http';
const transport = new HttpTransport('http://graphql-swapi.parseapp.com/');
transport.send(`
    {
      allFilms {
        films {
          title
        }
      }
    }
`).then(response => {
    console.log(JSON.stringify(response, null, 2));
});
```

## Send Custom Request & Response

It's possible to send custom headers like this:

```js
const headers = {
    'my-headers': 'some-value'
};
const transport = new HttpTransport('/graphql', {
    headers,
    buildOptions: () => {
      // build you custom header here
    },
    formatResponse: (response) => {
      // format you response here
    }
})
```

## Authentication

This package does not handle authentication information for you. But it'll let you interact with your app's existing authentication mechanism.

* If you already have an authorized cookie, it'll be sent with the HTTP request. (supports CORS)
* You can also set a custom `Authorization` [header]((https://www.npmjs.com/package/basic-auth-header) to implement [basic-auth](https://www.npmjs.com/package/basic-auth) support.

## Error Handling

By default it will create and throw a new `Error` object using the first GraphQL error. Error handling can be customized with the `handleErrors` option. Check the deafult error handler in `lib/index.js` for an example.
