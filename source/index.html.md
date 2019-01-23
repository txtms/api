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

Welcome to the TxtMS API! You can use our API to access TxtMS API endpoints, which can get and post /orders, make text messages via WhatsApp, SMS and Fax.

We have language bindings in Shell, Ruby and Python. You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.


# Create Order and send text
> To post orders/ and send sms, whatsApp for fax messages


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
}' https://www.txtms.de/api/v1/orders

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
uri = URI('https://www.txtms.de/api/v1/orders')
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

webhook_url = 'https://www.txtms.de/api/v1/orders'
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

TxtMS uses API keys to allow access to the API. You can register a new TxtMS API key at our [Account Area](https://txtms.de/admin/accounts).

Txtms expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Api-Key: txtmstx7329&R2c`

If you wish to add more attributes, you can always add them as json in `data` attribute.

<aside class="notice">
You must replace <YOUR API KEY> with your personal API key.
</aside>

# Orders

## Get Orders

```ruby
require 'net/http'
url = URI('https://www.txtms.de/api/v1/orders/6')
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
req = urlreq.Request("https://www.txtms.de/api/v1/orders/1")
req.add_header('Api-Key', '<YOUR API-KEY>')
urlreq.urlopen(req).read()
```

```shell
curl "https://www.txtms.de/api/v1/orders/" -H "Api-Key: <YOUR API-KEY>"
```


This endpoint retrieves all orders, you can also define an ID to get only one.

### HTTP Request

`GET https://www.txtms.de/api/orders`

This endpoint retrieves last 10 orders, you can also define an ID to get only one.

#### URL Parameters

Parameter | Description
--------- | -----------
limit | define number of orders to be retrieved, default limit is 10
by_contact_id | orders of a specific contact
by_template_id | orders who are related to a specific template
by_group_id | orders who are related to a specific group
by_repeat | orders who have specific repart order (no repat, hourly, daily, weekly..etc)
by_delivery | orders which delivery is set to one of the options (sms, whatsApp or fax)
by_category | orders who are part of a specific category
by_title | ordres who have a specific title 
by_expires_at | orders who are going to be expired on a specific timestamp


e.g; `GET https://www.txtms.de/api/orders?by_group_id=123&limit=20`


#Contacts
The order is belongs to a specific contact, to be able to send a SMS, whatsApp text or fax you need to have a contact with proper attributes.

## Get a Specific Contact
```ruby
require 'net/http'
url = URI('https://www.txtms.de/api/v1/contacts/6')
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
req = urlreq.Request("https://www.txtms.de/api/v1/contacts/1")
req.add_header('Api-Key', '<YOUR API-KEY>')
urlreq.urlopen(req).read()
```

```shell
curl "https://www.txtms.de/api/v1/contacts/" -H "Api-Key: <YOUR API-KEY>"
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

This endpoint retrieves a specific contact.
`GET https://www.txtms.de/api/contacts/1`

### HTTP Request

`GET https://www.txtms.de/api/contacts`

This endpoint retrieves last 10 contacts, you can also define an ID to get only one as mentioned above.

#### Query Parameters

`GET https://www.txtms.de/api/contacts?`

Parameter     | Default | Description
--------------| ------- | -----------
limit         |10 | define number of orders to be retrieved, default limit is 10
email_adr     |'' | If set to any email, the result will also include contact(s) with the given email.
first_name    |'' | If set to any name, the result will also include contact(s) with the given parameter.
last_name     |'' | If set to any last_name, the result will also include contact(s) with the given parameter.
sms_tel       |'' | If set to any sms tel number, the result will also include contact(s) with the given parameter.
whatsapp_tel  |'' | If set to any WhatsApp tel number, the result will also include contact(s) with the given parameter.

<aside class="success">
Example: https://www.txtms.de/api/orders?email=bob@gmail.com&sms_tel=01700200200
</aside>


#Groups
Using groups you can set specific set of configurations like welcome messages farewells, specific events and etc

## Get a Specific Group
```ruby
require 'net/http'
url = URI('https://www.txtms.de/api/v1/groups/1')
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
req = urlreq.Request("https://www.txtms.de/api/v1/groups/1")
req.add_header('Api-Key', '<YOUR API-KEY>')
urlreq.urlopen(req).read()
```

```shell
curl "https://www.txtms.de/api/v1/groups/" -H "Api-Key: <YOUR API-KEY>"
```

> You can add any parameter from the above Query parameters to the example. e.g; /groups?limit=10
> The above command returns JSON structured like this:


```json
{
  
}
```

This endpoint retrieves a specific group.
`GET https://www.txtms.de/api/groups/1`

### HTTP Request

`GET https://www.txtms.de/api/groups`

This endpoint retrieves last 10 groups, you can also define an ID to get only one as mentioned above.

#### Query Parameters

`GET https://www.txtms.de/api/groups?`

Parameter     | Default | Description
--------------| ------- | -----------
limit         |10 | define number of orders to be retrieved, default limit is 10
by_name     |'' | If set to any name, the result will also include groups(s) with the given name.

<aside class="success">
Example: https://www.txtms.de/api/groups?by_name=foobar
</aside>

#Templates
Using templates you can create sms text templates which enables you to add extra information to the main text.

## Get a Specific Template
```ruby
require 'net/http'
url = URI('https://www.txtms.de/api/v1/templates/1')
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
req = urlreq.Request("https://www.txtms.de/api/v1/templates/1")
req.add_header('Api-Key', '<YOUR API-KEY>')
urlreq.urlopen(req).read()
```

```shell
curl "https://www.txtms.de/api/v1/templates/" -H "Api-Key: <YOUR API-KEY>"
```

```json
{
  
}
```

This endpoint retrieves a specific template.
`GET https://www.txtms.de/api/templates/1`

### HTTP Request

`GET https://www.txtms.de/api/templates`

This endpoint retrieves last 10 contacts, you can also define an ID to get only one as mentioned above.


You can add any parameter from the above Query parameters to the example. e.g; `/templates?by_name=xyz`

The command returns JSON structured, see the side bar.

#### Query Parameters

`GET https://www.txtms.de/api/templates?`

Parameter     | Default | Description
--------------| ------- | -----------
limit         |10 | define number of orders to be retrieved, default limit is 10
by_name     |'' | If set to any name, the result will also include template(s) with the given name.

<aside class="success">
Example: `https://www.txtms.de/api/templates?by_name=foobar
</aside>