# SMSGlobal node SDK


![Build](https://github.com/smsglobal/smsglobal-node/workflows/Build/badge.svg?branch=master)
[![codecov](https://codecov.io/gh/smsglobal/smsglobal-node/branch/master/graph/badge.svg)](https://codecov.io/gh/smsglobal/smsglobal-node)
[![Node](https://img.shields.io/node/v/smsglobal)](https://www.npmjs.com/package/smsglobal)
[![npm](https://img.shields.io/npm/v/smsglobal)](https://www.npmjs.com/package/smsglobal)
[![Downloads](https://img.shields.io/npm/dm/smsglobal.svg)](https://www.npmjs.com/package/smsglobal)


The SMSGlobal Node library provides convenient access to the SMSGlobal REST API from node applications.

Sign up for a [free SMSGlobal account](https://www.smsglobal.com/mxt-sign-up/?utm_source=dev&utm_medium=github&utm_campaign=node_sdk) today and get your API Key from our advanced SMS platform, MXT. Plus, enjoy unlimited free developer sandbox testing to try out your API in full!


## Example
 Check out the [code examples](examples)


## SMSGlobal rest API credentials

Rest API credentials can be provided in the SMSGlobal client or node environment variables. The credential variables are `SMSGLOBAL_API_KEY` and `SMSGLOBAL_API_SECRET`


## Installation

```
npm install --save smsglobal
```


## Usage

* Require `smsglobal` in your file

```
const apiKey = 'YOUR_API_KEY';
const apiSecret = 'YOUR_API_SECRET';
var smsglobal = require('smsglobal')(apiKey, secret);
```

> All method return promise if no callback is given

### To send a sms
```js
var payload = {
    origin: 'from number',
    destination: 'destination',
    message: 'This is a test message'
}

smsglobal.sms.send(payload, function (error, response) {
    console.log(response);
});
```
### To fetch a list outgoing sms

```js
var promise = smsglobal.sms.getAll();

promise
    .then(function(response) {
        console.log(response)
    })
    .catch(function(error){
        console.log(error)
    });
```

### To fetch an outgoing sms by id

```js
var id = 'outgoing-sms-id';
var promise = smsglobal.sms.get(id);

promise
    .then(function(response) {
        console.log(response)
    })
    .catch(function(error){
        console.log(error)
    });
```

### To fetch a list incoming sms

```js
var promise = smsglobal.sms.incoming.getAll();

promise
    .then(function(response) {
        console.log(response)
    })
    .catch(function(error){
        console.log(error)
    });
```

### To fetch an incoming sms by id

```js
var id = 'incoming-sms-id';
var promise = smsglobal.sms.incoming.get(id);

promise
    .then(function(response) {
        console.log(response)
    })
    .catch(function(error){
        console.log(error)
    });
```


### To send an OTP
```js
var payload = {
  origin: 'from number',
  message: '{*code*} is your SMSGlobal verification code.',
  destination: 'destination'
};

// {*code*} placeholder is mandatory and will be replaced by an auto generated numeric code.

smsglobal.otp.send(payload, function(error, response) {
  if (response) {
    console.log(response);
  }

  if (error) {
     console.log(error);
  }
});

```

*Success response object*

```js
{
  statusCode: 200,
  status: 'OK',
  data: {
    requestId: '404372541683676561917558',
    validUnitlTimestamp: '2020-11-18 17:08:14',
    createdTimestamp: '2020-11-18 16:58:14',
    lastEventTimestamp: '2020-11-18 16:58:14',
    status: 'Sent'
  }
}
```

*Error response object in the case of validation error*

```js
{
  statusCode: 400,
  status: 'Bad Request',
  data: {
    errors: {
      message: {
        errors: [
          'Message template should contain a placeholder for code i.e. {*code*}.'
        ]
      }
    }
  }
}

```

### To cancel an OTP request

```js
var id = 'otp-request-id'; // requestId received upon sending an OTP
var promise = smsglobal.otp.cancel(id)

promise.then((response) => {
   console.log(response)
}).catch((err) => {
   console.log(error)
});
```

### To verify an OTP code entered by your user

```js
var id = 'otp-request-id'; // requestId received upon sending an OTP
var code = 'otp-code'; // input code entered by your user

smsglobal.otp.verify(id, code, function(error, response) {
  if (response) {
    console.log(response);
  }

  if (error) {
     console.log(error);
  }
});
```

### To fetch an OTP request

```js
var id = 'otp-request-id'; // requestId received upon sending an OTP
var promise = smsglobal.otp.get(id);

promise
    .then(function(response) {
        console.log(response)
    })
    .catch(function(error){
        console.log(error)
    });

```

### To fetch a list of OTP requests

The `getAll` method accepts two arguments first one is filter options and second one is a callback method. Both arguments are optional. Following exampels illustrate different ways of using it.


*Filter options argument*

```js
var options = { status: 'Verfied'};

var promise = smsglobal.otp.getAll(options);

promise
    .then(function(response) {
        console.log(response)
    })
    .catch(function(error){
        console.log(error)
    });
```

#### *Callback method arguments*

```js
smsglobal.otp.getAll(function (error, response) {
    console.log(response);
});

```
#### *Filter options and callback method arguments*

```
var options = { status: 'Verfied'};

smsglobal.otp.getAll(options, function (error, response) {
    console.log(response);
});
```


## Running tests

Run the tests:

```
npm test
```

To run test with code coverage report

```
npm run mocha-only
```

## Following endpoints are covered
* [sms](https://www.smsglobal.com/rest-api/?utm_source=dev&utm_medium=github&utm_campaign=node_sdk#api-endpoints)
* [sms-incoming](https://www.smsglobal.com/rest-api/?utm_source=dev&utm_medium=github&utm_campaign=node_sdk#api-endpoints)
* [OTP](https://www.smsglobal.com/rest-api/?utm_source=dev&utm_medium=github&utm_campaign=node_sdk#api-endpoints)

# Reference
[REST API Documentation](https://www.smsglobal.com/rest-api/?utm_source=dev&utm_medium=github&utm_campaign=node_sdk)

For any query [contact us](https://www.smsglobal.com/contact/?utm_source=dev&utm_medium=github&utm_campaign=node_sdk)
