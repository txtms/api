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
curl -H "Content-Type: application/json" -H "Api-Key: <YOUR API KEY>" --data '{\
  "title": "first order post",\
  "description": "Your order description",\
  "template_id": "<Template ID>",\
  "data": {\
    "image": "www.txtms.de/order.jpg",\
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

# if you wanna send to an existing contact instead of contact_attributes just pass e.g; "contact_id": 123.
```


```ruby
# ruby POST request to txtms api endpoint
require 'net/http'
require 'json'
order_data = {
  "title": "first order post",
  "description": "Your order description",
  "template_id": "<Template ID>", #Optional
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
req = Net::HTTP::Post.new(uri.path, 'Content-Type': 'application/json', 'Api-Key': '<YOUR API KEY>')
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
  "template_id": "<Template ID>", #optional
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
    headers={'Content-Type': 'application/json', Api-Key': '<YOUR API KEY>'}
)
if response.status_code != 200:
    raise ValueError(
        'Request to slack returned an error %s, the response is:\n%s'
        % (response.status_code, response.text)
    )
```


> Make sure to replace `<YOUR API KEY>` with your API key.
>
> You can alwasy add more extra fields as json in data.

TxtMS uses API keys to allow access to the API. You can register a new TxtMS API key at our [Account Area](http://txtms.de/accounts).

Txtms expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: meowmeowmeow`

<aside class="notice">
You must replace <code><YOUR API KEY></code> with your personal API key.
</aside>

# Orders/Leads

## Get Orders

```ruby
require 'net/http'
url = URI('http://www.txtms.de/api/v1/orders/6')
req = Net::HTTP::Get.new(url.path)
req.add_field("Api-Key", "<YOUR API-KEY>")
response = Net::HTTP.new(url.host, url.port).start do |http| 
  http.request(req) 
end
response.body

#Completed 403 Forbidden in 1086ms (Views: 1083.6ms | ActiveRecord: 0.3ms)
```

```python
try:
    import urllib2 as urlreq # Python 2.x
except:
    import urllib.request as urlreq # Python 3.x
req = urlreq.Request("http://www.txtms.de/api/v1/orders/1")
req.add_header('Api-Key', '<YOUR API-KEY>')
urlreq.urlopen(req).read()
```

```shell
curl "http://www.txtms.de/api/v1/orders/" -H "Api-Key: <YOUR API-KEY>"
```


This endpoint retrieves all orders/leads, you can also define an ID to get only one.

### HTTP Request

`GET http://www.txtms.de/api/orders`

This endpoint retrieves all contacts, you can also define an ID to get only one.

### HTTP Request

`GET http://www.txtms.de/api/contacts?`

### Query Parameters
:, :, :, :, :
Parameter     | Default | Description
--------------| ------- | -----------
email_adr     |'' | If set to any email, the result will also include contact(s) with the given email.
first_name    |'' | If set to any name, the result will also include contact(s) with the given parameter.
last_name     |'' | If set to any last_name, the result will also include contact(s) with the given parameter.
sms_tel       |'' | If set to any sms tel number, the result will also include contact(s) with the given parameter.
whatsapp_tel  |'' | If set to any WhatsApp tel number, the result will also include contact(s) with the given parameter.

<aside class="success">
Example: `http://www.txtms.de/api/orders?email="bob@gmail.com&sms_tel=01700200200`
</aside>

## Get a Specific Contact
```ruby
require 'net/http'
url = URI('http://www.txtms.de/api/v1/contacts/6')
req = Net::HTTP::Get.new(url.path)
req.add_field("Api-Key", "<YOUR API-KEY>")
response = Net::HTTP.new(url.host, url.port).start do |http| 
  http.request(req) 
end
response.body

#Completed 403 Forbidden in 1086ms (Views: 1083.6ms | ActiveRecord: 0.3ms)
```

```python
try:
    import urllib2 as urlreq # Python 2.x
except:
    import urllib.request as urlreq # Python 3.x
req = urlreq.Request("http://www.txtms.de/api/v1/contacts/1")
req.add_header('Api-Key', '<YOUR API-KEY>')
urlreq.urlopen(req).read()
```

```shell
curl "http://www.txtms.de/api/v1/contacts/" -H "Api-Key: <YOUR API-KEY>"
```

> You can add any parameter from the above Query parameters to the example. e.g; `/contacts?email=bob@gmail.com`
> The above command returns JSON structured like this:

```json
{
  id: 1,
  salutation: "Mr",
  name: "Bob",
  lastname: "Doe",
  sms_phone: "00291758417720",
  fax: "00291758417721",
  whatsapp_phone: "00291758417722",
  email: "bob@doe.com",
  message_delivery: "sms",
  birthday: "1986-10-16T00:00:00.000Z",
  order_id: null,
  group_id: null,
  data: {
  address: "",
  city: "",
  postal_code: ""
  },
  account_id: 2,
  created_at: "2019-01-09T22:57:05.674Z",
  updated_at: "2019-01-09T22:57:05.674Z"
}
```

This endpoint retrieves a specific TxtMS.

<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

### HTTP Request

`GET http://www.txtms.de/api/v1/orders?`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the order to retrieve
by_contact_id | orders of a specific contact
by_template_id | orders who are related to a specific template
by_group_id | orders who are related to a specific group
by_repeat | orders who have specific repart order (no repat, hourly, daily, weekly..etc)
by_delivery | orders which delivery is set to one of the options (sms, whatsApp or fax)
by_category | orders who are part of a specific category
by_title | ordres who have a specific title 
by_expires_at | orders who are going to be expired on a specific timestamp




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
curl "http://www.txtms.de/api/TxtMSs/2"
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

`DELETE http://www.txtms.de/TxtMSs/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the TxtMS to delete

