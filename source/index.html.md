---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - ruby
  - python


includes:
  - errors

search: true
---

# Introduction

Welcome to the TxtMS API! You can use our API to access TxtMS API endpoints, which can get and post leads/orders, make text messages via WhatsApp, SMS and Fax.

We have language bindings in Shell, Ruby. You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.


# Create Order and send text

> To post orders/leads and send sms, whatsApp for fax messages


```shell
# With shell, you can just pass the correct header with each request
curl -H "Content-Type: application/json" -H "api_key: <YOUR API KEY>" --data '{\
  "title": "first order post",\
  "description": "Your order description",\
  "account_id": "<YOUR ACCOUNT ID>",\
  "template_id": "<Template ID>",\
  "data": {\
    "image": "example.com/order.jpg",\
    "comments": "extra information"\
  },\
  "category": "general",\
  "delivery": "sms",\
  "repeat": "monthly",\
  "duration": "3",\
  "dispatch_time": "25/10/2018 13:00",\
  "expires_at": "30/10/2018",\
  "contact_attributes": {\
    "salutation": "Mr",\
    "name": "John",\
    "lastname": "Doe",\
    "sms_phone": "324234",\
    "fax": "23423423",\
    "whatsapp_phone": "23423432",\
    "email": "api@ds.de",\
    "birthday": "12-12-1986",\
    "group_id": "<GROUP ID>",\
    "data": { #optional\
      "profile_image": "contact.jpg",\
      "foo": "bar"\
    }\
  }\
}' http://www.txtms.de/api/v1/orders

# if you wanna send to an existing contact instead of contact_attributes just pass e.g; "contact_id": 123
```


```ruby
# ruby POST request to txtms api endpoint
require 'net/http'
require 'json'
order_data = {
  "title": "first order post",
  "description": "Your order description",
  "account_id": "<YOUR ACCOUNT ID>",
  "template_id": "<Template ID>",
  "data": {
    "image": "order.jpg",
    "comments": "extra information"
  },
  "category": "general",
  "delivery": "sms",
  "repeat": "monthly",
  "duration": "3",
  "dispatch_time": "25/10/2018 13:00",
  "expires_at": "30/10/2018",
  "contact_attributes": {
    "salutation": "Mr",
    "name": "John",
    "lastname": "Doe",
    "sms_phone": "324234",
    "fax": "23423423",
    "whatsapp_phone": "23423432",
    "email": "api@ds.de",
    "birthday": "12-12-1986",
    "group_id": "<GROUP ID>",
    "data": { #optional
      "profile_image": "contact.jpg",
      "foo": "bar"
    }
  }
}
uri = URI('http://www.txtms.de/api/v1/orders')
http = Net::HTTP.new(uri.host, uri.port)
req = Net::HTTP::Post.new(uri.path, 'Content-Type': 'application/json', 'api_key': '<YOUR API KEY>')
req.body = order_data.to_json
res = http.request(req)
puts "response #{res.body}"
rescue => e
puts "failed #{e}"
```


```python
# python POST request to txtms api endpoint
import json
import requests

webhook_url = 'http://www.txtms.de/api/v1/orders'
order_data = {
  "title": "first order post",
  "description": "Your order description",
  "account_id": "<YOUR ACCOUNT ID>",
  "template_id": "<Template ID>",
  "data": {
    "image": "order.jpg",
    "comments": "extra information"
  },
  "category": "general",
  "delivery": "sms",
  "repeat": "monthly",
  "duration": "3",
  "dispatch_time": "25/10/2018 13:00",
  "expires_at": "30/10/2018",
  "contact_attributes": {
    "salutation": "Mr",
    "name": "John",
    "lastname": "Doe",
    "sms_phone": "324234",
    "fax": "23423423",
    "whatsapp_phone": "23423432",
    "email": "api@ds.de",
    "birthday": "12-12-1986",
    "group_id": "<GROUP ID>",
    "data": { #optional
      "profile_image": "contact.jpg",
      "foo": "bar"
    }
  }
}

# if you wanna send to an existing contact instead of contact_attributes just pass e.g; "contact_id": 123

response = requests.post(
    webhook_url, data=json.dumps(order_data),
    headers={'Content-Type': 'application/json', api_key': '<YOUR API KEY>'}
)
if response.status_code != 200:
    raise ValueError(
        'Request to slack returned an error %s, the response is:\n%s'
        % (response.status_code, response.text)
    )
```


> Make sure to replace `API_KEY` with your API key.
>
> You can add any extra fields as json in data.

TxtMS uses API keys to allow access to the API. You can register a new TxtMS API key at our [Account Area](http://txtms.de/accounts).

Txtms expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: meowmeowmeow`

<aside class="notice">
You must replace <code><YOUR API KEY></code> with your personal API key.
</aside>

# Kittens

## Get All Kittens

```ruby
require 'kittn'

api = Txtms::APIClient.authorize!('meowmeowmeow')
api.TxtMSs.get
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.TxtMSs.get()
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

