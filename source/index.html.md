---
title: API Reference

language_tabs: # must be one of https://github.com/rouge-ruby/rouge/wiki/List-of-supported-languages-and-lexers
  - javascript

toc_footers:
  - <a href='https://nebulox.io/register'>Sign Up for an API Key</a>

includes:
  - errors

search: true

code_clipboard: true

meta:
  - name: description
    content: Documentation for the Nebulox API
---

# Introduction

Welcome to the Nebulox API! You can use our API to access Nebulox API endpoints.

We have language bindings in Python and JavaScript! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

# Invoice

## Create Invoice


```javascript
const axios = require('axios');

axios.post('https://cryptogateway-quby-dev.nginhub.com/api/invoice/create', {
    apiKey: 'YOUR_API_KEY',
    price: '100',
    orderId: 'YOUR_ORDER_ID',
    baseCurrency: 'usd',
    coinSymbol: 'BTC',
    networkName: 'Bitcoin'
  })
  .then(function (response) {
    console.log(response);
  })
  .catch(function (error) {
    console.log(error);
  });
```

> If every thing you sent is correct you will get a response like bellow with status code 201:

```json
{
  "message": "Operation was successful.",
  "result": {
      "price": 10,
      "orderId": "DGK-324324",
      "status": "PENDING",
      "gatewayId": "41c6fe17-b72f-4923-9da2-dc7a91173e73",
      "userId": "d6646cf8-0b65-4d7d-ab2b-02e8dcd1ede3",
      "addressId": null,
      "amount": null,
      "coinId": null,
      "networkId": null,
      "info": null,
      "id": "5c5a7933-51ad-4542-b0b6-9157552e8230",
      "created_at": "2023-02-13T12:18:00.672Z",
      "updated_at": "2023-02-13T12:18:00.672Z",
      "url": "https://nebulox.io/invoice/5c5a7933-51ad-4542-b0b6-9157552e8230"
  },
  "meta": {}
}
```

> If you send an invalid apiKey you will get response by status 406:

```json
{
    "message": "This gateway is not active",
    "result": [],
    "meta": {}
}
```

This endpoint will create an invoice for your gateway.

### HTTP Request

`POST https://cryptogateway-quby-dev.nginhub.com/api/invoice/create`


### Request Body

Key | Type | Required | Description
--------- | ------- | ----------- | -----------
apiKey | string | true |The identifier of your gateway.
price | number | true | Price of your invoice.
orderId | string | true | Order identifier in your database.
baseCurrency | string | false | You can choose between `eur` AND `usd`.
coinSymbol | string | false | The destination coin you want to have in your wallet. Only `BTC` for now.
networkName | string | false | The network you want to receive coin from. Only `Bitcoin` for now.

