---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - ruby


includes:
  - errors

search: true
---

# Introduction

Welcome to the TxtMS API! You can use our API to access TxtMS API endpoints, which can get and post leads/orders, make text messages via WhatsApp, SMS and Fax.

We have language bindings in Shell, Ruby. You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.


# Authentication

> To post orders/leads and send sms, whatsApp for fax messages

```ruby
# -*- coding: utf-8 -*-
TODO: fix the example
API_URL = 'http://www.txtms.de/api/v1/orders'


 conn = Faraday.new(url: API_URL) do |faraday|
    faraday.request  :url_encoded
    faraday.adapter  Faraday.default_adapter
  end

  conn.basic_auth(API_BASIC_AUTH_USER, API_BASIC_AUTH_PASS)

  response = conn.post do |req|
    req.url "/orders"
    req.headers['Content-Type'] = 'application/json'
    req.body = order.to_json
  end

  response
```


```shell
# With shell, you can just pass the correct header with each request
curl -H "Content-Type: application/json" --data '{"title":"test order2","description":"Your order description","account_id":1,"template_id":1,"data":{"image":"order.jpg","comments":"extra information"},"category":"general","delivery":"sms","repeat":"monthly","duration":"3","dispatch_time":"25/10/2018 13:00","expires_at":"30/10/2018","contact_id":1}' http://www.txtms.de/api/v1/orders
```


> Make sure to replace `API_KEY` with your API key.

TxtMS uses API keys to allow access to the API. You can register a new TxtMS API key at our [Account Area](http://txtms.de/accounts).

Txtms expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: meowmeowmeow`

<aside class="notice">
You must replace <code>meowmeowmeow</code> with your personal API key.
</aside>

# Kittens

## Get All Kittens

```ruby
require 'kittn'

api = Txtms::APIClient.authorize!('meowmeowmeow')
api.TxtMSs.get
```



```shell
curl "http://example.com/api/TxtMSs"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let TxtMSs = api.TxtMSs.get();
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

This endpoint retrieves all TxtMSs.

### HTTP Request

`GET http://example.com/api/TxtMSs`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
include_cats | false | If set to true, the result will also include cats.
available | true | If set to false, the result will include TxtMSs that have already been adopted.

<aside class="success">
Remember — a happy TxtMS is an authenticated TxtMS!
</aside>

## Get a Specific Kitten

```ruby
require 'kittn'

api = Txtms::APIClient.authorize!('meowmeowmeow')
api.TxtMSs.get(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.TxtMSs.get(2)
```

```shell
curl "http://example.com/api/TxtMSs/2"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.TxtMSs.get(2);
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

This endpoint retrieves a specific TxtMS.

<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

### HTTP Request

`GET http://example.com/TxtMSs/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the TxtMS to retrieve

## Delete a Specific Kitten

```ruby
require 'kittn'

api = Txtms::APIClient.authorize!('meowmeowmeow')
api.TxtMSs.delete(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.TxtMSs.delete(2)
```

```shell
curl "http://example.com/api/TxtMSs/2"
  -X DELETE
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.TxtMSs.delete(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "deleted" : ":("
}
```

This endpoint deletes a specific TxtMS.

### HTTP Request

`DELETE http://example.com/TxtMSs/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the TxtMS to delete

