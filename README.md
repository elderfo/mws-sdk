mws-sdk-promises
======

[![Build Status](https://travis-ci.org/elderfo/mws-sdk.svg?branch=master)](https://travis-ci.org/elderfo/mws-sdk)

Originally forked from [ticadia/mws-sdk](https://github.com/ticadia/mws-sdk).

What is done:
-------------

 - It is uses [request](https://www.npmjs.com/package/request). it is more flexible and there is no eventEmitter syntax.

 - Promises to provide generic async support.
 
 - I've add some new requests from updated Amazone API.
 
 - I fix it with better set params ability... so it now looks niceier!!!


Use it. Contribute to it.

it can be seamlessly used in ES2015/2016 way using [babel.js](https://babeljs.io/).
with new javascript code features like `yield` or `async` `wait` to put some sugar on your code. 

Examples
--------

Initialize

```javascript
var MWS = require('elderfo-mws-sdk-promises');
var client = new MWS.Client('accessKeyId', 'secretAccessKey', 'merchantId', {});
var marketplaceId = "ATVPDKIKX0DER";
```

now you can use it 

```javascript
function getListOrders(client, args) {
  var req = MWS.Orders.requests.ListOrders();
  req.set('CreatedAfter', args.CreatedAfter);
  req.set('CreatedBefore', args.CreatedBefore);
  req.set('LastUpdatedAfter', args.LastUpdatedAfter);
  req.set('MarketplaceId', args.MarketplaceId);
  req.set('LastUpdatedBefore', args.LastUpdatedBefore);
  req.set('OrderStatus', args.OrderStatus);
  req.set('FulfillmentChannel', args.FulfillmentChannel);
  req.set('PaymentMethod', args.PaymentMethod);
  req.set('BuyerEmail', args.BuyerEmail);
  req.set('SellerOrderId', args.SellerOrderId);
  req.set('MaxResultsPerPage', args.MaxResultsPerPage);
  return client.invoke(req);
}
// or you can do like this
function getListOrders(client, args) {
  var req = MWS.Orders.requests.ListOrders();
  req.set(args);
  return client.invoke(req);
}

```

Use it.

```javascript
var date = new Date();
getListOrders(client, {
  MarketplaceId: MarketplaceId,
  MaxResultsPerPage: 10,
  CreatedAfter: new Date(2015, 1, 1),
  CreatedBefore: new Date(2015, 1, 31)
})
.catch(function(error) {
  console.error(error);
})
.then(function(RESULT){
  console.log("--------");
  console.log(JSON.stringify(RESULT));
  console.log("--------");
});
```

Tests
-----

1. Create a file `.env` in the root directory and add and fill out the following:

  ```
  MerchantId=
  AccessKey=
  MarketPlaceId=
  SecretKey=
  ```
  
2. Run `npm test` or `yarn run test` to execute tests. (Note: you can turn on a test watcher by running `start run test:watch` or `yarn run test:watch`)
