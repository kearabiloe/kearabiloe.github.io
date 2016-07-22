---
title: API Reference

language_tabs:
  - shell

toc_footers:
  - <a href='https://crowdcoin.co.za/developers'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

The Crowdcoin API is REST-like and relies on HTTP status codes to indicate API errors. We support CORS so that you can interact with our API through a client-side web application. We return JSON in all responses from the API.

- API Overview: authentication, error codes, pagination and webhooks
- Transaction: query the status of transactions that were made against your merchant account

# Authentication

> To authorize, use this code:


```shell
curl "https://crowdcoin.co.za/api/v1/"
  -H "Authorization: ApiKey <username>:<api_key>"
```

> Make sure to replace `username:api_key` with your API key.

Crowdcoin uses API keys to allow access to the API. You can request a new Crowdcoin API key at our [developer portal](http://crowdcoin.co.za/developers).

Crowdcoin expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: ApiKey <username>:<api_key>`

<aside class="notice">
You must replace <code>username:api_key</code> with your personal username and API key.
</aside>

# Transactions

## Get All Transactions


```shell
curl "https://crowdcoin.co.za/api/v1/transaction/"
  -H "Authorization: ApiKey <username>:<api_key>"
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 1,
    "description": "INVOICE2345",
    "amount": 160,
    "status": {
	"code":"T200",
	"name":"APPROVED",
	"description":"Transaction approved"
	},
    "transaction_type": {
	"name":"AIRTIME_PAYMENT"
	}
  },
  {
    "id": 2,
    "description": "CALEDONIA",
    "amount": 10.99,
    "status": {
	"code":"T100",
	"name":"PENDING",
	"description":"Transaction is pending payment"
	},
    "transaction_type": {
	"name":"PAYMENT_LEAD"
	}
  }
]
```

This endpoint retrieves all Transactions.

### HTTP Request

`GET https://crowdcoin.co.za/api/v1/transaction/`


## Get a Specific Transaction


```shell
curl "https://crowdcoin.co.za/api/v1/transaction/2"
  -H "Authorization: ApiKey <username>:<api_key>"
```

> The above command returns JSON structured like this:

```json
  {
    "id": 2,
    "description": "CALEDONIA",
    "amount": 10.99,
    "status": {
	"code":"T100",
	"name":"PENDING",
	"description":"Transaction is pending payment"
	},
    "transaction_type": {
	"name":"PAYMENT_LEAD"
	}
  }
```

This endpoint retrieves a specific transaction.


### HTTP Request

`GET https://crowdcoin.co.za/api/v1/transaction/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the transaction to retrieve


## Webhook
We recommend that you make use of a webhook to be notified of payment completiong due to the real-time nature of the system. During your account set up we can configure a URL to which we will POST payment objects as we determine their status. We will only notify you of completed and errored payments through the webhook.

We `POST` the data as an `application/x-www-form-urlencoded` JSON string under the `object` key.

