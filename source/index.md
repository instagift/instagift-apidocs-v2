---
title: Instagift API Reference

language_tabs:
  - cURL

includes:
  - errors

search: true
---

# API Overview

This API provides Instagift merchants and users the ability to read and interact
with select Instagift data. The API is JSON only, and closely follows to format of
<a href="http://jsonapi.org/" target="_blank">JSON API</a>.

## Authentication

> Sample request including user authentication headers

```cURL
curl https://api.instagift.com/v2/sample/endpoint \
  -H "X-User-Email: person@example.com" \
  -H "X-User-Token: quhZKsGMSJc5eUAYm-FA" \
```

> Sample request including merchant authentication headers

```cURL
curl https://api.instagift.com/v2/sample/endpoint \
  -H "X-Merchant-Key: OWqqv2rwnWucQC22CVwvMg" \
  -H "X-Merhcant-Secret: 1WngOCryMpl1l7fXH7DIYA"
```

Both User and Merchant accounts of Instagift can authenticate by setting a combination of two HTTP request headers
('X-User-Email' and 'X-User-Token' for users and 'X-Merchant-Key' and 'X-Merchant-Secret' for merchants).
Throughout this doc,
endpoints and query filters will be marked as
<code class="prettyprint user">USER</code>,
<code class="prettyprint merchant">MERCHANT</code>, or
<code class="prettyprint public">PUBLIC</code>
depending on the type of authorization required.

Note: Throughout this doc, cURL examples will not include sample authentication headers.

### User Authentication HTTP Headers

Parameter | Required | Description
--------- | --------- | -----------
X-User-Email | true | A valid email for an Instagift user account
X-User-Token | true | See [Request User Token](#request-user-token)

### Merchant Authentication HTTP Headers

Parameter | Required | Description
--------- | --------- | -----------
X-Merchant-Key | true | Generated from the Merchant Dashboard
X-Merchant-Secret | true | Generated from the Merchant Dashboard

## Support

Please email [support@instagift.com](mailto:support@instagift.com) with all questions and issues.

Additionally, the source for this guide is publicy available on GitHub. Feel free to
submit pull requests if you find any typos or missing data, we'll do our best to keep
it updated.

* [https://github.com/mikesch/instagift-apidocs-v2](https://github.com/mikesch/instagift-apidocs-v2)

## Rate Limiting

Coming soon


<!--
################################################################################
-->


# Table of Contents

## Public Endpoints

The following API endpoints are accessible without user or merchant authentication.

Endpoint | Description
--------- | -----------
POST /v2/users | [Create a User](#create-a-user)
POST /v2/tokens | [Request User Token](#request-user-token)
DELETE /v2/tokens | [Reset User Token](#reset-user-token)
POST /v2/passwords | [Reset User Password](#reset-password)
GET /v2/merchants/:merchant_id | [Fetch a Merchant](#fetch-a-merchant)
GET /v2/locations/:location_id | [Fetch a Location](#fetch-a-location)
GET /v2/products/:product_id | [Fetch a Product](#fetch-a-product)
GET /v2/product_options/:product_option_id | [Fetch a Product Option](#fetch-a-product-option)
POST /v2/support_tickets | [Create a Support Ticket](#create-a-support-ticket)

## User Endpoints

The following API endpoints are accessible with valid user authentication, see
[Request User Token](#request-user-token).

Endpoint | Description
--------- | -----------
DELETE /v2/tokens | [Reset Token](#reset-user-token)
GET /v2/users/:user_id | [Get User Details](#)
GET /v2/certificates | [Get Certificates Collection](#)
GET /v2/certificates/:certificate_id | [Get Certificate Details](#)
POST /v2/certificates/:certificate_id/certificates | [Split Certificate Value](#)
POST /v2/certficates/:certificate_id/redemptions | [Redeem Certificate](#)
GET /v2/redemptions | [Get Redemptions Collection](#)
GET /v2/redemptions/:redemption_id | [Get Redemption Details](#)
POST /v2/certificates/:certificate_id/gifts | [Send Gift](#)
GET /v2/gifts | [Get Gift Collection](#)
GET /v2/gifts/:gift_id | [Get Gift Details](#)

## Merchant Endpoints

The following API endpoints are accessible with valid merchant authentication.
Merchant's can generate API keys from their Instagift Merchant Dashboard.
<a href="https://instagift.com/#pricing" target="_blank">GROW plan required</a>

Endpoint | Description
--------- | -----------
GET /v2/certificates | [List all Certificates](#)
GET /v2/certificates/{certificates.id} | [Fetch a Certificate by ID](#)
POST /v2/certificates/{certificates.id}/redemptions | [Redeem a Certificate by ID](#)
GET /v2/claim_codes/{certificates.claim_code} | [Fetch a Certificate by Claim Code](#)
POST /v2/claim_codes/{certificates.claim_code}/redemptions | [Redeem Certificate by Claim Code](#)
GET /v2/redemptions | [List all Redemptions](#)
GET /v2/redemptions/{redemptions.id} | [Fetch a Redemption by ID](#)


<!--
################################################################################
-->


# Certificates


## Fetch a Certificate

> Sample request

```cURL
curl https://api.instagift.com/v2/certificates/AzoXEYPYxG3OUaKJi234WQ
```

> Sample response

```json
{
    "links": {
        "certificates.user": "/v2/users/{certificates.user}",
        "certificates.parent": "/v2/certificates/{certificates.parent}",
        "certificates.merchant": "/v2/merchants/{certificates.merchant}",
        "certificates.product": "/v2/merchants/{certificates.product}"
    },
    "certificates": [
        {
            "id": "hD65TJvxnv8oIuyOmD056w",
            "href": "/v2/certificates/hD65TJvxnv8oIuyOmD056w",
            "product_type": "GiftCertificate",
            "claim_code": "62DD-CV4T-R2NTM2",
            "redeem_code": "R2NTM2",
            "status": "assigned",
            "marked_as_printed": false,
            "can_split_value": true,
            "qrcode_image": "/system/qrcodes/hD65TJvxnv8oIuyOmD056w.png",
            "currency": "USD",
            "face_value_cents": 10000,
            "price_cents": 10000,
            "seller": "Tuscan Kitchen",
            "title": "$100 Tuscan Kitchen eGift Card",
            "thumb": null,
            "merchant": {
                "id": "_P07R17NtAZhxN56rneT7A",
                "href": "/v2/merchants/_P07R17NtAZhxN56rneT7A",
                "url": "http://tuscankitchen.instagift.com/",
                "name": "Tuscan Kitchen",
                "time_zone": "Eastern Time (US & Canada)",
                "logo": "/logos/original/missing.png",
                "locations": [
                    {
                        "id": "108esJv3En11Ugc6VZLyCA",
                        "href": "/v2/locations/108esJv3En11Ugc6VZLyCA",
                        "display": "Tuscan Kitchen, 100 Main St., Ste 2, Pleasantville, KS",
                        "name": "Tuscan Kitchen",
                        "address1": "100 Main St.",
                        "address2": "Ste 2",
                        "city": "Pleasantville",
                        "state": "KS",
                        "zip": "67502",
                        "phone": "3166620036",
                        "lat": null,
                        "lng": null
                    }
                ]
            },
            "daily_deal_store": null,
            "product": {
                "id": "NnjAQSTtcMcHYZXhRehPVQ",
                "href": "http://tuscankitchen.instagift.com/gift-card",
                "type": "GiftCertificate",
                "discount_sale_name": null,
                "is_giveaway": false,
                "can_split_value": true,
                "gift_card_image": null,
                "photos": [],
                "headline": null,
                "tagline": "Tuscan Kitchen eGift Card",
                "terms": [
                    "Good on any food or drink",
                    "Can be used on tax and gratuity",
                    "Does not expire",
                    "Merchant are not required to give change for the unused balance"
                ],
                "expiration_instructions": "Unless otherwise noted, this gift card NEVER EXPIRES",
                "redemption_instructions": "This gift card can be redeemed at the locations listed at http://tuscankitchen.instagift.com/gift-card",
                "merchant_instructions": "This gift card originated from the Instagift.com online store for Tuscan Kitchen located at http://tuscankitchen.instagift.com/ Your staff should be trained to accept and validate gifts cards as they arrive. If you have questions, please ask your manager or e-mail support@instagift.com",
                "product_options": [
                    {
                        "id": "mJ1Ie-LkebfAtiCeaCIgFg",
                        "href": "/v2/product_options/mJ1Ie-LkebfAtiCeaCIgFg",
                        "currency": "USD",
                        "face_value_cents": 10000,
                        "price_cents": 10000,
                        "tagline": "$100 Gift Card",
                        "count": null,
                        "limit_per_order": null,
                        "is_recommended": false
                    }
                ],
                "redemption_locations": [
                    {
                        "id": "108esJv3En11Ugc6VZLyCA",
                        "href": "/v2/locations/108esJv3En11Ugc6VZLyCA",
                        "display": "Tuscan Kitchen, 100 Main St., Ste 2, Pleasantville, KS",
                        "name": "Tuscan Kitchen",
                        "address1": "100 Main St.",
                        "address2": "Ste 2",
                        "city": "Pleasantville",
                        "state": "KS",
                        "zip": "67502",
                        "phone": "3166620036",
                        "lat": null,
                        "lng": null
                    }
                ]
            },
            "product_option": {
                "id": "mJ1Ie-LkebfAtiCeaCIgFg",
                "href": "/v2/product_options/mJ1Ie-LkebfAtiCeaCIgFg",
                "currency": "USD",
                "face_value_cents": 10000,
                "price_cents": 10000,
                "tagline": "$100 Gift Card",
                "count": null,
                "limit_per_order": null,
                "is_recommended": false
            },
            "links": {
                "user": "7_JyTOaJuGD5ahUdWGvcnw",
                "parent": null,
                "merchant": "_P07R17NtAZhxN56rneT7A",
                "product": "NnjAQSTtcMcHYZXhRehPVQ"
            },
            "expires_at": null,
            "created_at": "2014-10-09T16:29:44Z",
            "updated_at": "2014-10-09T16:29:44Z"
        }
    ]
}
```

`GET /v2/certificates/:certificate_id` <code class="prettyprint user">USER</code> <code class="prettyprint merchant">MERCHANT</code>

### Response

Certificate relationships are expanded when fetching an individual certificate (vs list)
in order to efficiently provide all the data necessary to display a certificate for redemption.

Parameter | Description
--------- | -----------
href | Resource URL for this certificate, will respond to GET requests
product_type | GiftCertificate, Deal, or Event
claim_code | Can be used to transfer certificate between user accounts
redeem_code | Used by the merchant to redeem certificates
status | Possible statuses: assigned, cancelled, gifted, pending, redeemed, cancelled, returned
marked_as_printed | Certificate owner (user) has specified that he/she has printed the certificate
can_split_value | true/false. Certificate face value can be split into smaller denominations
qrcode_image | URL to QR Code image
currency | Currently only USD
face_value_cents | Amount the certificate can be redeemed for
price_cents | Amount paid for the certificate
seller | Name of the seller, convenient for display
title | Title of the product, convenient for display
thumb | Small image of the product / merchant, convenient for display
expires_at | Datetime the certificate can no longer be redeemed for full face value.
daily_deal_store | Third party store information if the seller of this certificate was a daily deal store.

### Relationships

Name | Description
--------- | --------- | -----------
[user](#fetch-a-user) | User details for the certificate owner
[parent](#fetch-a-certificate) | Present if this certificate was created due to a partial redemption or split
[merchant](#fetch-a-merchant) | Merchant details for this certificate
[product](#fetch-a-product) | Product details for this certificate

## List all Certificates

> Sample request(s)

```cURL
curl https://api.instagift.com/v2/certificates
curl https://api.instagift.com/v2/certificates?status=available&product_type=Event&page=2
```

> Sample response

```json
{
    "links": {
        "certificates.user": "/v2/users/{certificates.user}",
        "certificates.parent": "/v2/certificates/{certificates.parent}",
        "certificates.merchant": "/v2/merchants/{certificates.merchant}",
        "certificates.product": "/v2/merchants/{certificates.product}"
    },
    "meta": {
        "href": "?per_page=10&page=1",
        "page": 1,
        "per_page": 10,
        "page_count": 1,
        "total_count": 13,
        "links": {
            "first": "?per_page=10&page=1",
            "previous": null,
            "next": null,
            "last": "?per_page=10&page=1"
        }
    },
    "certificates": [
        {
            "id": "sD-2VrA6hxAj8FVnoSc_gw",
            "parent_id": null,
            "href": "/v2/certificates/sD-2VrA6hxAj8FVnoSc_gw",
            "product_type": "GiftCertificate",
            "claim_code": "E69W-CDQ2-WTWH6Y",
            "redeem_code": "WTWH6Y",
            "status": "assigned",
            "marked_as_printed": false,
            "can_split_value": true,
            "qrcode_image": "/system/qrcodes/sD-2VrA6hxAj8FVnoSc_gw.png",
            "currency": "USD",
            "face_value_cents": 10000,
            "price_cents": 10000,
            "seller": "Tuscan Kitchen",
            "title": "$100 Tuscan Kitchen eGift Card",
            "thumb": null,
            "links": {
                "user": "srX0Fin8wFfJ1TEcffTj0w",
                "merchant": "NNA6XfwMj9XUCf58V1_u-Q",
                "product": "tQpEkvBp2E0oH1zRiP6RLQ",
                "product_option": "RjOWgOhoYf-SETVcyMjJEw"
            },
            "expires_at": null,
            "created_at": "2014-10-08T18:15:21Z",
            "updated_at": "2014-10-08T18:15:21Z"
        },
        {
            "...": "..."
        }
    ]
}
```

`GET /v2/certificates` <code class="prettyprint user">USER</code> <code class="prettyprint merchant">MERCHANT</code>

### HTTP Parameters

Parameter | Required | Description
--------- | --------- | -----------
status | false | Possible statuses: 'all' and 'available'. Defaults to all. <code class="prettyprint user">USER</code>
product_type | false | Possible product_types: 'Deal', 'Event', 'GiftCertificate'. Defaults to all types. <code class="prettyprint user">USER</code>
page | false | 1 to n. Defaults to 1.

### Response

Relationships are not expanded in list view. See [Fetch a Certificate](#fetch-a-certificate) for expanded response.

## Split a Certificate

> Sample request(s)

```cURL
curl -X POST https://api.instagift.com/v2/certificates/eSilaL3ev7w3UXvssQ_xFA/certificates \
-H "Content-Type: application/json" \
-d '{"new_face_value_cents":"4000"}' \
```

> Sample response

```json
{
    "links": {
        "certificates.parent": "/v2/certificates/{certificates.parent}",
        "...": "..."
    },
    "certificates": [
        {
            "id": "TZkfX5yZgWGPVyVHi8FVqg",
            "href": "/v2/certificates/TZkfX5yZgWGPVyVHi8FVqg",
            "face_value_cents": 6000,
            "...": "...",
            "links": {
                "parent": null,
                "...": "..."
            }
        },
        {
            "id": "NArlAnTTTnXrL1n_DWJA9w",
            "href": "/v2/certificates/NArlAnTTTnXrL1n_DWJA9w",
            "face_value_cents": 4000,
            "...": "...",
            "links": {
                "parent": "TZkfX5yZgWGPVyVHi8FVqg",
                "...": "..."
            }
        }
    ]
}
```

`POST /v2/certificates/:certificate_id/certificates` <code class="prettyprint user">USER</code>

### HTTP Parameters

Parameter | Required | Description
--------- | --------- | -----------
face_value_cents | false | Possible product_types: 'Deal', 'Event', 'GiftCertificate'. Defaults to all types. <code class="prettyprint user">USER</code>

### Response

In a successful split, two unexpanded [certificate objects](#list-all-certificates) are returned.
The child certificate will have a parent relationship pointing to the original certificate.

## Redeem a Certificate

> Sample request(s)

```cURL
curl -X POST https://api.instagift.com/v2/certificates/eSilaL3ev7w3UXvssQ_xFA/gifts \
-H "Content-Type: application/json" \
-d '{"amount_to_redeem_cents":"4000"}' \
```

> Sample response

```json
{
    "links": {
        "...": "..."
    },
    "redemptions": [
        {
            "id": "f_OGwyVpgEBgRf-nh-0faA",
            "href": "/v2/redemptions/f_OGwyVpgEBgRf-nh-0faA",
            "amount_cents": 10000,
            "...": "..."
        }
    ]
}
```

`POST /v2/certificates/:certificate_id/redemptions` <code class="prettyprint user">USER</code> <code class="prettyprint merchant">MERCHANT</code>

### HTTP Parameters

Parameter | Required | Description
--------- | --------- | -----------
amount_to_redeem_cents | false | Amount to redeem. If none is passed, the entire certificate face value is redeemed.

### Response

`201 Created` See [Fetch a Redemption](#fetch-a-redemption)

### Relationships

See [Fetch a Redemption](#fetch-a-redemption)

## Gift a Certificate

> Sample request(s)

```cURL
curl -X POST http://api.instagift.com/v2/certificates/fBkhLlMVLUYpFOjkAvMTbQ/gifts \
    -H "Content-Type: application/json" \
    -d '{"gift":{"sender_name": "Sender Schmidt", "sender_reply_to": "sender@example.com", "recipient_name": "Receiver Rogers", "recipient_email": "receiver@example.com", "message": "Enjoy this gift!"}}' \
```

> Sample response

```json
{
    "links": {
        "...": "..."
    },
    "gifts": [
        {
            "id": "Kk8dw5jSaf2oyzLMet9CLA",
            "href": "/v2/gifts/Kk8dw5jSaf2oyzLMet9CLA",
            "...": "..."
        }
    ]
}
```

`POST /v2/certificates/:certificate_id/gifts` <code class="prettyprint user">USER</code>

### HTTP Parameters

Parameter | Required | Description
--------- | --------- | -----------
gift | true | A JSON object containing the gift information. {"gift":{"sender_name": "John Doe", "recipient_email": "receiver@example.com"}
gift.sender_name | true | Name of the certificate owner who is sending the gift
gift.sender_reply_to | false | Reply email address of the certificate owner who is sending the gift
gift.recipient_name | false | Gift recipient's name
gift.recipient_email | true | Email address where to send the gift
gift.message | false | Personal message to include in the gift email
gift.send_date | false | Date when the gift should be sent. All future gifts send at or around 3AM ET on date specified. Defaults to immediate send.

### Response

`201 Created` See [Fetch a Gift](#fetch-a-gift)

### Relationships

See [Fetch a Gift](#fetch-a-gift)


<!--
################################################################################
-->

# Claim Codes

## Fetch a Certificate by Claim Code

`GET /v2/claim_code/:claim_code` <code class="prettyprint merchant">MERCHANT</code>

## Redeem a Certificate by Claim Code

`POST /v2/claim_codes/:claim_code/redemptions` <code class="prettyprint merchant">MERCHANT</code>

## Claim a Certificate by Claim Code

`PUT /v2/claim_codes/:claim_code/certificates` <code class="prettyprint user">USER</code>


<!--
################################################################################
-->


# Comps

## Send Comps to an Email(s)
Coming soon

# Customers

## Create a Customer
Coming soon
## List all Customers
Coming soon
## Fetch a Customer
Coming soon
## Comp a Customer
Coming soon


<!--
################################################################################
-->


# Gifts

## Fetch a Gift

> Sample request

```cURL
curl http://api.instagift.com/v2/gifts/Kk8dw5jSaf2oyzLMet9CLA/gifts
```

> Sample response

```json
{
    "links": {
        "gifts.certificate": "/v2/certificates/{gifts.certificate}",
        "gifts.sender": "/v2/users/{gifts.sender}",
        "gifts.recipient": "/v2/users/{gifts.recipient}"
    },
    "gifts": [
        {
            "id": "Kk8dw5jSaf2oyzLMet9CLA",
            "href": "/v2/gifts/Kk8dw5jSaf2oyzLMet9CLA",
            "sender_name": "Sender Schmidt",
            "sender_reply_to": "sender@example.com",
            "recipient_name": "Receiver Rogers",
            "recipient_email": "recipient@example.com",
            "message": "I hope you enjoy a night out on me!",
            "send_date": null,
            "claimed_at": null,
            "last_sent_at": "2014-10-09T18:42:31Z",
            "attempts": 1,
            "failure_count": 0,
            "links": {
                "certificate": "uNgmH1EPY6VKj3khdRFo0w",
                "sender": "ypRuj-KYopAl_yF2PqXlfg",
                "recipient": null
            },
            "created_at": "2014-10-09T18:42:30Z",
            "updated_at": "2014-10-09T18:42:31Z"
        }
    ]
}
```

`GET /v2/gifts/:gift_id` <code class="prettyprint user">USER</code>

### Response

Parameter | Description
--------- | -----------
href | Resource URL for this gift, will respond to GET requests
sender_name | Name of the certificate owner who is sending the gift
sender_reply_to | Reply email address of the certificate owner who is sending the gift
recipient_name | Gift recipient's name
recipient_email | Email address where to send the gift
message | Personal message to include in the gift email
send_date | Date when the gift should be sent. All future gifts send at or around 3AM ET on date specified. Defaults to immediate send.
claimed_at | Datetime when the recipient claims the gift. null until claimed
last_sent_at |  Datetime indicating the last time Instagift attempted to deliver the gift email
attempts | Number of times the gift has been sent
failure_count | Number of times the gift failed to send

### Relationships

Name | Description
--------- | --------- | -----------
[certificate](#fetch-a-certificate) | Certificate being gifted
[sender](#fetch-a-user) | User who sent the gift
[recipient](#fetch-a-user) | User who received the gift. Null until claimed.

## List all Gifts

> Sample request

```cURL
curl http://api.instagift.com/v2/gifts
```

> Sample response

```json
{
    "links": {
        "...": "..."
    },
    "gifts": [
        {
            "id": "Kk8dw5jSaf2oyzLMet9CLA",
            "href": "/v2/gifts/Kk8dw5jSaf2oyzLMet9CLA",
            "...": "..."
        },
        {
            "...": "..."
        }
    ]
}
```

`GET /v2/gifts` <code class="prettyprint user">USER</code>

### Response

An array of [gift objects](#fetch-a-gift)


<!--
################################################################################
-->


# Locations

## Fetch a Location

> Sample request

```cURL
curl https://api.instagift.com/v2/locations/AzoXEYPYxG3OUaKJi234WQ
```

> Sample response

```json
```

`GET /v2/locations/:location_id` <code class="prettyprint public">PUBLIC</code>

### Response

Parameter | Description
--------- | -----------
href | Resource URL for this location, will respond to GET requests

### Relationships

Name | Description
--------- | --------- | -----------
[merchant](#fetch-a-merchant) | Merchant details for this certificate

<!--
################################################################################
-->


# Merchants

## Fetch a Merchant

> Sample request

```cURL
curl https://api.instagift.com/v2/merchants/AzoXEYPYxG3OUaKJi234WQ
```

> Sample response

```json
```

`GET /v2/merchants/:merchant_id` <code class="prettyprint public">PUBLIC</code>

### Response

Parameter | Description
--------- | -----------
href | Resource URL for this merchant, will respond to GET requests

### Relationships

Name | Description
--------- | --------- | -----------
[locations](#fetch-a-location) | Merchant details for this certificate

<!--
################################################################################
-->


# Passwords

## Reset Password

> Sample request

```cURL
curl -X POST http://api.instagift.com/v2/passwords \
  -H "Content-Type: application/json" \
  -d '{"email":"person@example.com"}' \

```

> Sample response

```json
{
  "data": {
    "title": "Password reset sent",
    "email": "person@example.com"
  }
}
```

`POST /v2/passwords` <code class="prettyprint public">PUBLIC</code>

### HTTP Parameters

Parameter | Required | Description
--------- | --------- | -----------
email | true | A valid email address for an Instagift user account


### Response

`201 Created`


<!--
################################################################################
-->


# Products

## Fetch a Product

> Sample request

```cURL
curl https://api.instagift.com/v2/products/AzoXEYPYxG3OUaKJi234WQ
```

> Sample response

```json
```

`GET /v2/products/:product_id` <code class="prettyprint public">PUBLIC</code>

### Response

Parameter | Description
--------- | -----------
href | Resource URL for this product, will respond to GET requests

### Relationships

Name | Description
--------- | --------- | -----------
[merchant](#fetch-a-merchant) | Merchant details for this certificate
[location](#fetch-a-location) | Location details for each product redemption location
[product_options](#fetch-a-product-option) | Pricing/purchase options for this product


<!--
################################################################################
-->


# Product Options

## Fetch a Product Option

> Sample request

```cURL
curl https://api.instagift.com/v2/locations/AzoXEYPYxG3OUaKJi234WQ
```

> Sample response

```json
```

`GET /v2/locations/:location_id` <code class="prettyprint public">PUBLIC</code>

### Response

Parameter | Description
--------- | -----------
href | Resource URL for this certificate, will respond to GET requests

### Relationships

Name | Description
--------- | --------- | -----------
[merchant](#fetch-a-merchant) | Merchant details for this certificate


<!--
################################################################################
-->


# Redemptions

## Fetch a Redemption

> Sample request(s)

```cURL
curl https://api.instagift.com/v2/redemptions/f_OGwyVpgEBgRf-nh-0faA
```

> Sample response

```json
{
    "links": {
        "redemptions.certificate": "/v2/certificates/{redemptions.certificate}",
        "redemptions.user": "/v2/users/{redemptions.user}",
        "redemptions.merchant": "/v2/merchants/{redemptions.merchant}",
        "redemptions.location": "/v2/locations/{redemptions.location}"
    },
    "redemptions": [
        {
            "id": "f_OGwyVpgEBgRf-nh-0faA",
            "href": "/v2/redemptions/f_OGwyVpgEBgRf-nh-0faA",
            "amount_cents": 10000,
            "amount_paid_cents": 10000,
            "source": "api-v2-user",
            "links": {
                "certificate": "-3qdxkN_aoAwoX4byOLmrQ",
                "user": "IRxn4SmMQlDjM7bVlIfl5w",
                "merchant": "WnDQkpaFftq5w1G8PX2Rpg",
                "location": "DBVMHAdRRRjdfUFGJZzRPw"
            },
            "created_at": "2014-10-09T18:08:43Z",
            "updated_at": "2014-10-09T18:08:43Z"
        }
    ]
}
```

`GET /v2/redemptions/:redemption_id` <code class="prettyprint user">USER</code> <code class="prettyprint merchant">MERCHANT</code>

### Response

Parameter | Description
--------- | -----------
href | Resource URL for this redemption, will respond to GET requests
amount_cents | Amount redeemed in cents
amount_paid_cents | Amount paid for the redeemed certificate (if it was purchased at discount)
source | Used by the merchant to redeem certificates

### Relationships

Name | Description
--------- | --------- | -----------
[certificate](#fetch-a-certificate) | Certificate that was redeemed
[user](#fetch-a-user) | User details for the redeemer
[merchant](#fetch-a-merchant) | Merchant where the certificate was redeemed
[location](#fetch-a-location) | Location where the certificate was redeemed

## List all Redemptions

> Sample request

```cURL
curl http://api.instagift.com/v2/redemptions
```

> Sample response

```json
{
    "links": {
        "...": "..."
    },
    "redemptions": [
        {
            "id": "f_OGwyVpgEBgRf-nh-0faA",
            "href": "/v2/gifts/f_OGwyVpgEBgRf-nh-0faA",
            "...": "..."
        },
        {
            "...": "..."
        }
    ]
}
```

`GET /v2/redemptions` <code class="prettyprint user">USER</code> <code class="prettyprint merchant">MERCHANT</code>

### Response

An array of [redemption objects](#fetch-a-redemption)


<!--
################################################################################
-->


# Support Tickets

## Create a Support Ticket
Coming soon


<!--
################################################################################
-->


# Users

## Create a User

## Fetch a User


<!--
################################################################################
-->


# Tokens

## Request User Token

> Sample request

```cURL
curl -X POST http://api.instagift.com/v2/tokens \
  -H "Content-Type: application/json" \
  -d '{"user":{"email":"person@example.com","password":"testing1234"}}'
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
      "name": "Tester Joe",
      "authentication_token": "quhZKsGMSJc5eUAYm-FA",
      "last_login_at": "2014-07-09T01:41:41Z"
    }
  ]
}
```

`POST /v2/tokens` <code class="prettyprint public">PUBLIC</code>

### HTTP Parameters

Parameter | Required | Description
--------- | --------- | -----------
user | true | A JSON object of a user’s credentials. { user: { email: "person@example.com", password: "testing1234" } }
user.email | true | Email address to authenticate
user.password | true | User's password

### Response

Parameter | Description
--------- | -----------
href | Resource URL for this user, will respond to GET requests
email | User's email address, used for API authentication
authentication_token | Token used for API authentication
last_login_at | Datetime of last login

### Relationships

Name | Description
--------- | --------- | -----------
[certificates](#certificates) | A collection of certificates for this user
[redemptions](#redemptions) | A collection of redemption for this user
[gifts](#gifts) | A collection of gifts for this user


## Reset User Token

> Sample request

```cURL
curl -i -X DELETE http://api.instagift.com/v2/tokens \
  -H "Content-Type: application/json" \
  -H "X-User-Email: person@example.com" \
  -H "X-User-Token: quhZKsGMSJc5eUAYm-FA" \
```

`DELETE /v2/tokens` <code class="prettyprint user">USER</code>

### Response

`204 No Content`

