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
This will create a Developer API Key through which it is
possible to interact with the platform.

The Developer API Key looks like the following:

`Developer API Key: OPENPLATFORM`

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

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
```

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
```

> Make sure to replace `meowmeowmeow` with your API key.

Kittn uses API keys to allow access to the API. You can register a new Kittn API key at our [developer portal](http://example.com/developers).

Kittn expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: meowmeowmeow`

<aside class="notice">
You must replace <code>meowmeowmeow</code> with your personal API key.
</aside>

# Connecting OPEN to an Application

Before connecting to an Application there are a
few components to understand. These components are maintained
in the off-chain OPEN library to ensure easy
transitions and to provide built-in frameworks and functionality for the
OPEN Community. For more information go to the OPEN Library.

## Receipts
A receipt specifies the transaction information, the user name,
the OPEN State, and is signed by the address that performed the operation.
It is an off-chain representation of the transaction and is used by the application
for verification.

## Products
The OPEN States reference off-chain components, these are the Products.
They detail pricing, descriptions, and other product information.

## Server Side
The majority of the server side of OPEN deals primarily with accepting and verifying OPEN States, and by sending Product Data information via request. Examining the product information identifier in your application and making the corresponding change is left up to the developer.

### Reading Receipts
Parsing receipts into specific categories

### Validating Receipts
Checking on-chain dependencies
Verify Its Signature

### Responding to Product Requests
Sending information on product (pricing, ect) when requested by users

## User Side
Along with the product UI for the application,
it is also necessary to User has product UI.

### Requesting list of Products

### Requesting Product Information

### Purchasing a Product
User is able to purchase by calling purchase (having the price loaded in-app)
and setting the details of the product verification in-app ()
Transaction must be sent to Scaffold with details in msg (and need and address)

POST Scaffold (payment) (state)

Creating a Receipt
POST User Update (UID) (state) (signed transaction with address)

Sending a Receipt
POST User Update (UID) (state) (signed transaction with address)

# Interacting with Scaffolds
The primary means of interacting with the Scaffolds is through
the OPEN Developer Dashboard, it is also possible to make changes
using the OPEN API.
CRUD Operations with Scaffold
GET Scaffold list
CRUD Operations for Products in Scaffold Catalogue
POST Scaffold State Catalogue (Operation)
POST Scaffold Set Price (address, arg)

# OPEN Library
As the OPEN Platform grows we intend to devote more time
and resources to making the platform as usable as possible.
Along with dependencies like web3.js, the OPEN Library features
Packages intended to make the transition as easy as possible.

## Packages
### Product
#### Catalogue
#### Product
#### Unit (unique product identifier)
### Receipt
Receipt
Receipt Operator
Transaction
Transaction
Scaffold (off-chain representation)
OPEN State (off-chain representation)

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```shell
curl "http://example.com/api/kittens"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let kittens = api.kittens.get();
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 1,
    "name": "Fluffums",
    "breed": "calico",
    "fluffiness": 6,
    "cuteness": 7
  },
  {
    "id": 2,
    "name": "Max",
    "breed": "unknown",
    "fluffiness": 5,
    "cuteness": 10
  }
]
```

### HTTP Request

`GET http://example.com/api/kittens`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
include_cats | false | If set to true, the result will also include cats.
available | true | If set to false, the result will include kittens that have already been adopted.

<aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside>

## Get a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get(2)
```

```shell
curl "http://example.com/api/kittens/2"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.get(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "name": "Max",
  "breed": "unknown",
  "fluffiness": 5,
  "cuteness": 10
}
```

This endpoint retrieves a specific kitten.

<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

### HTTP Request

`GET http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to retrieve

## Delete a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.delete(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.delete(2)
```

```shell
curl "http://example.com/api/kittens/2"
  -X DELETE
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.delete(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "deleted" : ":("
}
```

This endpoint deletes a specific kitten.

### HTTP Request

`DELETE http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to delete
