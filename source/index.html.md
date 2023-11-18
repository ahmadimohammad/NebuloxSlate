---
title: API Reference

language_tabs: # must be one of https://github.com/rouge-ruby/rouge/wiki/List-of-supported-languages-and-lexers
  - javascript
  - php

toc_footers:
  - <a href='https://nebulox.io/app/user/register' ><h3>Sign Up for an API Key</h3></a>
  - <hr>
  - <a href='https://api.nebulox.io/docs'><h3>Swagger</h3></a>
  - <a href='https://www.postman.com/cloudy-shuttle-20631/workspace/nebulox-public-api/overview'><h3>Postman</h3></a>

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


## Nebulox Crypto Gateway
Nebulox Gateway simplifies cryptocurrency transactions for businesses. By creating a gateway with essential details, including a Webhook URL, it facilitates real-time notifications. Valid transactions trigger automatic webhook alerts, delivering comprehensive details instantly. This user-friendly system ensures seamless integration, making cryptocurrency payments straightforward and efficient.


# API Key

with An API Key you can seamlessly integrate with Nebulox's Crypto payment gateway services. follow these steps to acquire an API key: 


**Create an Account:** Start by creating an account on Nebulox.io using this [registration link](https://nebulox.io/app/user/register).

**Access Gateway Setup:** In your dashboard, navigate to the gateway section in the side menu. Click on the "Setup Your Free Gateway" button to create your first gateway.

**Provide Gateway Details:** Fill in some simple inputs: 
  - Business Name
  - Payment Expiration Time 
  - Website URL
  - Webhook URL
  - Business Logo file(optional).


**Create Gateway:** Click on the create [gateway button](https://nebulox.io/app/gateway) 


## Save Your API Key

**Integrate Nebulox's APIs:** Once the gateway is created, you will be provided with an API key in a dialogue box. Utilize this unique API key for integrating Nebulox's APIs into your applications.


**Copy and Save Your API Key:** Copy and securely save this API key. Note that once saved, you won't have access to it again. In case of loss, you can regenerate a new API key.


**Confirm API Key:** Click on the confirmation button indicating that you have saved the API key.
 


# Webhook URL

## Setting Up Webhooks


>if your Webhook URL is valid, you will be posted a payload like this: 

```json
{
  "orderId": "dpkg-1234",
  "txId": "cf2efce87f85a16e4bac7d0b3cdd548700f074fa375c0640b0da02155266d200",
  "amount": "6.9",
  "confirmations": 1,
  "status": "COMPLETED"
}
```


The configuration of a new Nebulox gateway necessitates the provision of a mandatory webhook URL. By providing a valid webhook URL during this setup, you empower Nebulox to relay real-time notifications regarding new transactions. This not only facilitates a seamless integration process but also lays the foundation for automated operations within your payment processing flow.


### Receive Webhook Notifications:

Once you've set up your URL, Nebulox will send you a heads-up whenever a new transaction happens with your provided address. When a transaction occurs, Nebulox sends a POST request to the specified webhook URL with a payload that includes details of the transaction.


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
    amount:'0.0025'
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
          'amount' :'0.0025'
        ]
    ]
);

$headers = $response->getHeaders();
$body = $response->getBody();

var_dump($headers, $body);
```

> If everything you sent is correct you will get a response like bellow with status code 201:

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
      "amount": 0.0025,
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
`amount` | number | Yes | Order's amount.

<aside class="notice">
  Note:
  <li> <b>baseCurrency</b> must be in [<code>EUR</code>, <code>USD</code>]. </li>
  <li> <b>coinSymbol</b> must be in [<code>BTC</code>,<code>ETH</code>,<code>USDT</code>,<code>TRX</code>]. </li>
  <li> <b>networkName</b> must be in [<code>Bitcoin</code>,<code>Ethereum</code>,<code>Tron</code>]. </li>
</aside>
