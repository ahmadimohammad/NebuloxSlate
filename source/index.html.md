---
title: API Reference

language_tabs: # must be one of https://github.com/rouge-ruby/rouge/wiki/List-of-supported-languages-and-lexers
  - javascript
  - php

toc_footers:
  - <a href='https://nebulox.io/register' ><h3>Sign Up for an API Key</h3></a>
  - <hr>
  - <a href='https://api.nebulox.io/docs'><h3>Swagger</h3></a>
  - <a href='https://nebulox.io/docs'><h3>Postman</h3></a>

includes:
  - errors

search: true

code_clipboard: true

meta:
  - name: description
    content: Documentation for the Nebulox API
---

# Introduction

Welcome to Nebulox's technical document.

Crypto payment gateway by Nebulox is leading solutions for Merchants and Business clients. It’s a decentralized Crypto payment gateway that enables businesses to accept transactions in Bitcoin and other crypto currencies. 

This payment API allows you to integrate & accept cryptocurrencies payments into your website. The Payment API links the checkout system of your business to a payment processing network that allows your clients to make transactions from you.

# Invoice

## Create Invoice


```javascript
const axios = require('axios');

axios.post('https://api.nebulox.io/api/invoice/create', {
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
    console.error(error);
  });
```

```php
$client = new GuzzleHttp\Client();

$response = $client->request(
    'POST',
    'https://api.nebulox.io/api/invoice/create',
    [
        'form_params' => [
          'apiKey': 'YOUR_API_KEY',
          'price': 100,
          'orderId': 'YOUR_ORDER_ID',
          'baseCurrency': 'USD',
          'coinSymbol': 'BTC',
          'networkName': 'Bitcoin'
        ]
    ]
);

$headers = $response->getHeaders();
$body = $response->getBody();

var_dump($headers, $body);
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

This payment crypto API allows you to integrate & accept cryptocurrency payments on your website. So create a payment!

### HTTP Request

`POST https://api.nebulox.io/api/invoice/create`


### Request Body

Key | Type | Required | Description
--------- | ------- | ----------- | -----------
`apiKey` | string | Yes |Merchant's API key which has been provided after gateway creation.
`price` | number | Yes | Order's price (in merchant's base currency - default: EUR).
`orderId` | string | Yes | Merchant's order unique identifier. It will be used to track order.
`baseCurrency` | string | No |Your price currency. (if not entered, it will be set to EUR).
`coinSymbol` | string | No | Your order payment coin, If you send us this parameter, your user will skip the select coin page.
`networkName` | string | No | Your order payment network, If you send us this parameter, your user will skip the select network page.

<aside class="notice">
  Note:
  <li> <b>baseCurrency</b> must be in [<code>EUR</code>, <code>USD</code>]. </li>
  <li> <b>coinSymbol</b> must be in [<code>BTC</code>,<code>ETH</code>,<code>USDT</code>,<code>TRX</code>]. </li>
  <li> <b>networkName</b> must be in [<code>Bitcoin</code>,<code>Ethereum</code>,<code>Tron</code>]. </li>
</aside>
