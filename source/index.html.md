---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - ruby
  - python
  - javascript

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>

includes:
  - errors

search: true
---

# Introduction

This API documentation is meant to give OPEN Developers an endpoint how to develop and interact with the OPEN Platform.

These documents specify how to get started with the OPEN Platform, how to create a Scaffold and pricing scheme, and how to integrating this pricing scheme into another application environment.

The point of the OPEN Platform is to make the transition as seamless as possible for the developer which means that many common pricing trends (product id, receipt) will persist.

# Getting Started
## Getting a Wallet
An important part of accepting cryptocurrency payments is to get a Wallet and address.
If you already have this feel free to skip this section.
While the OPEN Wallet is still in development, it is recommended that you use a hardware solution like Trezor or Ledger Nano.
In the context of this, it is possible to simply go through MetaMask.

## Setting up a Developer Account
Before interacting with the OPEN Platform, it is necessary to create an
account on the OPEN Platform initially.
Once you login in you can create a create a Developer API Key through which it is
possible to interact with the platform.

The Developer API Key looks like the following:

`Developer API Key: OPEN_DEV_PUB_KEY`


```shell
curl '/api/gen-developer-api-key'
```



## Creating a Scaffold
Once the Developer Account is created, Scaffolds and pricing schemes can be developed and deployed using the OPEN Scaffold Dashboard. This can be seen in more depth in the OPEN Demo.
Installing Dependencies
The OPEN API relies on several software dependencies, to ensure that the process is as easy and painless as possible.

# Authentication
Specific calls to the Scaffold require authentication from the developer.
This is why there exists two OPEN API keys
* Public Developer API Key (for testing purposes)
* Private Developer API Key (for authentication and security purposes on deployment)

> To authorize, use this code:


```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here"
  -H "open_dev_id: OPEN_DEV_PUB_KEY"
```


> Make sure to replace `OPEN_DEV_PUB_KEY` with your API key.


OPEN expects for the API key to be included in all API requests to the server in a
header that looks like the following:

`open_dev_id : OPEN_DEV_PUB_KEY`

<aside class="notice">
You must replace <code>OPEN_DEV_PUB_KEY</code> with your personal API key.
</aside>

# Scaffolds

> A Scaffold can be represented through the following JSON:

```json
  {
  "developerAddress": DEV_ADDRESS,
  "scaffoldDescription": DESCRIPTION,
  "fiatAmount": AMOUNT,
  "conversionCurrency": USD,
  "currencyConversionValue", VALUE
  }

```

The primary means of interacting with the Scaffolds is through
the OPEN Developer Dashboard, it is also possible to make changes
using the OPEN API.


## Deploy a Scaffold

This provides the endpoint to creating and deploying a Scaffold.

### HTTP Request

`POST  http://openapp.io/api/deploy-scaffold/:scaffold_data`

### Request Parameters

Parameter | Description
--------- | -----------
developerAddress | The Developer's Wallet Address.
scaffoldDescription | A brief description of the Scaffold's function.
fiatAmount | Currency value of the item.
conversionCurrency | The currency being converted (e.g. USD)
currencyConversionValue | The value in ETH of the desired currency.

## Get a Specific Scaffold

> An example of this call would be:

```shell
curl 'http://openapp.io/api/scaffold/OPEN_DEV_PUB_KEY/0x0'
```

> This call will return a Scaffold in JSON:

```json
  {
  "developerAddress": DEV_ADDRESS,
  "scaffoldDescription": DESCRIPTION,
  "fiatAmount": AMOUNT,
  "conversionCurrency": USD,
  "currencyConversionValue", VALUE
  }

```

This provides an endpoint for a developer to get a specific scaffold.

### HTTP Request

`GET http://openapp.io/api/scaffold/:openPublicKey/:contractAddress`


### Query Parameters

Parameter |  Description
--------- |  -----------
openPublicKey | This is the Developer's API key
contractAddress | The Address that the Scaffold Smart contract has been deployed to

## Get all Scaffolds

> An example of this call would be:

```shell
curl 'http://openapp.io/api/scaffolds'
```

> This call will return a list of Scaffolds in JSON:

```json
  [
  {
  "developerAddress": DEV_ADDRESS,
  "scaffoldDescription": DESCRIPTION,
  "fiatAmount": AMOUNT,
  "conversionCurrency": USD,
  "currencyConversionValue", VALUE
  }
  ]

```

This provides an endpoint for the developer to see all of the Scaffolds they own.

### HTTP Request
`GET http://openapp.io/api/scaffolds`


## Storing Scaffold Data Off-Chain
> Below is a Scaffold off-chain representation in json.

```json
{
  "open_dev_id": OPEN_DEV_PUB_KEY,
  "contract_address": CONTRACT_ADDRESS,
  "abiData": ABI_CODE,
  "scaffold": SCAFFOLD_DATA
}

```
There is a need to reference Scaffolds from off-chain components.
This is done by incorporating the Scaffold Data into a larger off-chain object
that can keep track of the contract code, and other necessary reference information.


# Connecting to an Application
Before connecting to an Application there are a
few components to understand. These components are maintained
in the off-chain OPEN library to ensure easy
transitions and to provide built-in frameworks and functionality for the
OPEN Community. For more information go to the OPEN Library.

### Server Side
The majority of the server side of OPEN deals primarily with accepting and verifying OPEN States,
and by sending Product Data information via request. Examining the product information identifier
in your application and making the corresponding change is left up to the developer.

### Client Side
Along with the product UI for the application,
it is also necessary to have the necessary dependencies for the user to request
product information and send transactions through the client side.

# OPEN Library
As the OPEN Platform grows we intend to devote more time
and resources to making the platform as usable as possible.
Along with dependencies like web3.js, the OPEN Library features
Packages intended to make the transition as easy as possible.

## Packages
* Receipt
* Product
* Scaffold
* OPEN State

# Products

```json
  {
  "productID": PRODUCT_ID,
  "contractAddress": SCAFFOLD_ADDRESS,
  "productType": PRODUCT_AMOUNT,
  "productPricing": PRICING_EXPRESSION
  }

```

The OPEN States reference off-chain components, these are the Products.
They detail pricing, descriptions, and other product information.

### Attributes

Attribute |  Description
--------- |  -----------
productID | The unique product identifier.
contractAddress | The address of the contract the Product is referenced in.
productType | The type of product (consumable, subscription)
productPricing | The price of the product.


## Getting a Product
```shell
curl 'http://openapp.io/api/scaffold/:contract_address/product/:product_id'
```

Get a specific product from a Scaffold


### HTTP Request

`GET http://openapp.io/api/scaffold/:contract_address/product/:product_id`


### Query Parameters

Parameter |  Description
--------- |  -----------
contract_address | The address that the Scaffold has been published to
product_id | The unique identifier for the product


## Getting a list of Products
```shell
curl 'http://openapp.io/api/scaffold/:contract_address/products'
```


Get a list of products associated with a Scaffold.

### HTTP Request
`GET http://openapp.io/api/scaffold/:contract_address/products`

### Query Parameters

Parameter |  Description
--------- |  -----------
contract_address | The address that the Scaffold has been published to


## Transactions

```json
  {
  "userAddress": USER_ADDRESS,
  "scaffoldAddress": SCAFFOLD_ADDRESS,
  "product_id": TRANSACTION_DATA,
  "funds": FUNDS
  }
```
Transactions are an off-chain representation of on-chain transactions. They are used
to pre-format the data that will be sent to the Scaffold.

Attribute |  Description
--------- |  -----------
userAddress | Address of the sender of the funds.
scaffoldAddress | Address of the Scaffold being sent the transaction.
productID | Identifier of the product in question
funds | Value sent in the transaction


## Receipts
```json
  {
  "userAddress": USER_ADDRESS,
  "scaffoldAddress": SCAFFOLD_ADDRESS,
  "transaction": TRANSACTION_DATA,
  "signed_transaction": SIGNED_INFORMATION
  }
```
A receipt specifies the transaction information, the user name,
the OPEN State, and is signed by the address that performed the operation.
It is an off-chain representation of the transaction and is used by the application
for verification.

#### Attributes

Attribute |  Description
--------- |  -----------
userAddress | Address of the sender of the funds.
scaffoldAddress | Address of the Scaffold being sent the transaction.
transaction | The transaction data.
signed_user_information | The signed transaction.




### Creating a Receipt

In Development

### Submitting a Receipt

In Development

### Reading a Receipt

In Development

### Validating a Receipt

In Development


# API Documentation Currently in Development

* CRUD Operations with Scaffold
* CRUD Operations with Receipts
* CRUD Operations for Products
* CRUD Operations for OPEN State
