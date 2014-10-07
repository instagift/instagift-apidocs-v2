---
title: API Reference

language_tabs:
  - shell

includes:
  - errors

search: true
---

# API Overview

Welcome to the Instagift API. This API exposes some select endpoints for interacting
with Instagift data. The API is JSON only, and closely follows to format of
<a href="http://jsonapi.org/" target="_blank">JSON API</a>.

### Authentication

### Rate Limiting

### Support

# Authentication

Both users and merchants can authenticate by setting a combination of two HTTP request headers
('X-User-Email' and 'X-User-Token' for users and 'X-Merchant-Key' and 'X-Merchant-Secret' for merchants).
Throughout this doc,
endpoints that require user and/or merchant authentication will be marked like this:

* User
* Merchant

Shell examples will not include authentication headers.

## Authenticating a User

> Sample request including user authentication headers

```shell
curl -X GET -H "Content-Type: application/json" \
  -H "X-User-Email: person@example.com" \
  -H "X-User-Token: quhZKsGMSJc5eUAYm-FA" \
  https://api.instagift.com/v2/sample/endpoint
```

Parameter | Required | Description
--------- | --------- | -----------
X-User-Email | true | A valid email for an Instagift user account
X-User-Token | true | See [Request User Token](#request-user-token)

### User Endpoints

Endpoint | Description
--------- | -----------
DELETE /v2/tokens | [Reset Token](#reset-user-token)
GET /v2/users/{users.id} | [Get User Details](#)
GET /v2/users/{users.id}/certificates | [Get Certificates Collection](#)
GET /v2/certificates/{certificates.id} | [Get Certificate Details](#)
POST /v2/certificates/{certificates.id}/certificates | [Split Certificate Value](#)
POST /v2/certficates/{certificates.id}/redemptions | [Redeem Certificate](#)
GET /v2/users/{users.id}/redemptions | [Get Redemptions Collection](#)
GET /v2/redemptions/{redemptions.id} | [Get Redemption Details](#)
POST /v2/certificates/{certificates.id}/gifts | [Send Gift](#)
GET /v2/users/{users.id}/gifts | [Get Gift Collection](#)
GET /v2/gifts/{gifts.id} | [Get Gift Details](#)

## Authenticating a Merchant

Merchant's can generate API keys in their Instagift Merchant Dashboard.

> Sample request including merchant authentication headers

```shell
curl -X GET -H "Content-Type: application/json" \
  -H "X-Merchant-Key: OWqqv2rwnWucQC22CVwvMg" \
  -H "X-Merhcant-Secret: 1WngOCryMpl1l7fXH7DIYA" \
  https://api.instagift.com/v2/sample/endpoint
```

### HTTP Headers

Include these HTTP headers in each API request for authentication.

Parameter | Required | Description
--------- | --------- | -----------
X-Merchant-Key | true | Generated from the Merchant Dashboard
X-Merchant-Secret | true | Generated from the Merchant Dashboard

### Merchant Endpoints

Merchants have access to the following API endpoints. Authentication required.

Endpoint | Description
--------- | -----------
GET /v2/merchants/{merchants.id}/certificates | [List all Certificates](#)
GET /v2/certificates/{certificates.id} | [Fetch a Certificate by ID](#)
POST /v2/certificates/{certificates.id}/redemptions | [Redeem a Certificate by ID](#)
GET /v2/claim_codes/{certificates.claim_code} | [Fetch a Certificate by Claim Code](#)
POST /v2/claim_codes/{certificates.claim_code}/redemptions | [Redeem Certificate by Claim Code](#)
GET /v2/merchants/{merchants.id}/redemptions | [List all Redemptions](#)
GET /v2/redemptions/{redemptions.id} | [Fetch a Redemption by ID](#)


# User Tokens


## Request User Token

> Sample request

```shell
curl -X POST -H "Content-Type: application/json" \
  -d '{"user":{"email":"person@example.com","password":"testing1234"}}' \
  http://api.instagift.com/v2/tokens
```
> Sample response

```json
{
  "links": {
    "user.certificates": "/v2/user/{users.id}/certificates",
    "user.redemptions": "/v2/user/{users.id}/redemptions",
    "user.gifts": "/v2/user/{users.id}/gifts"
  },
  "users": [
    {
      "id": "GddXpGdvs3V89PkUwCSoIg",
      "href": "/v2/users/GddXpGdvs3V89PkUwCSoIg",
      "email": "person@example.com",
      "name": "Mike Schmidt",
      "authentication_token": "quhZKsGMSJc5eUAYm-FA",
      "last_login_at": "2014-07-09T01:41:41Z"
    }
  ]
}
```

### HTTP Request

`POST https://api.instagift.com/v2/tokens`

### HTTP Parameters

Parameter | Required | Description
--------- | --------- | -----------
user | true | A JSON object of a user’s credentials. { user: { email: "person@example.com", password: "testing1234" } }

### Response

Parameter | Description
--------- | -----------
id | Unique identifier for this user
href | Resource URL for this user, will respond to GET requests
email | User's email address, used for API authentication
authentication_token | Token used for API authentication
last_login_at | Datetime of last login

### Relationships

Name | Description
--------- | --------- | -----------
certificates | A collection of certificates for this user
redemptions | A collection of redemption for this user
gifts | A collection of gifts for this user

## Reset User Token

# Passwords

## Reset Password

# Certificates

## List all Certificates
## Fetch a Certificate
## Redeem a Certificate
## Split a Certificate
## Gift a Certificate
## Claim a Certificate

# Redemptions

## List all Redemptions
## Fetch a Redemption

# Gifts

## List all Gifts for a User

# Merchant Access

# Claim Codes

## Fetch a Certificate by Claim Code
## Redeem a Certificate by Claim Code

# Support Tickets

## Create a Support Ticket

# Markdown Examples

`Authorization: meowmeowmeow`

<aside class="notice">
You must replace `meowmeowmeow` with your personal API key.
</aside>

<aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside>

<aside class="warning">If you're not using an administrator API key, note that some kittens will return 403 Forbidden if they are hidden for admins only.</aside>

