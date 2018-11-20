---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - json

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the Kittn API! You can use our API to access Kittn API endpoints, which can get information on various cats, kittens, and breeds in our database.

We have language bindings in Shell, Ruby, Python, and JavaScript! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

This example API documentation page was created with [Slate](https://github.com/lord/slate). Feel free to edit it and use it as a base for your own API's documentation.

# Authentication

> To authorize, use this code:


> Make sure to replace `YOUR_API_KEY` with your API key.

Kittn uses API keys to allow access to the API. You can register a new Kittn API key at our [developer portal](http://example.com/developers).

Kittn expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: YOUR_API_KEY`

<aside class="notice">
You must replace <code>meowmeowmeow</code> with your personal API key.
</aside>

# Sensors

## Get All Sensors

> Example response

```json
{
  "enclosureSensorIds": [
    2,
    3,
    8
  ],
  "plantSensorIds": [
    18,
    21,
    7
  ]
}
```

This endpoint returns all sensor types and their respected ids. To perform other CRUD operations, see <code>/sensors/enclosure</code> listed under Enclosure Sensors and <code>/sensors/plant</code> listed under Plant Sensors.

### HTTP Request

`GET http://api.stepbystepml.io/agm/v1/sensors`

# Enclosures

## Get All Enclosures

> Example response

```json
{
    "enclosures": 
        {
            "enclosureId": 12,
            "title": "Basement Enclosure 1",
            "length": 12.5,
            "width": 10.5,
            "height": 14,
            "location": "basement",
            "dateCreated": "2018-11-20 09:00:53"
        },
        {
            "enclosureId": 13,
            "title": "Basement Enclosure 2",
            "length": 12.5,
            "width": 10.5,
            "height": 14,
            "location": "basement",
            "dateCreated": "2018-12-20 09:00:53"
        }
}
```

Lists all enclosures associated with your account.

### HTTP Request

`GET http://api.stepbystepml.io/agm/v1/sensors`

## Get a Specific Enclosure

> Example response

```json
{
    "enclosureId": 12,
    "title": "Basement Enclosure 1",
    "length": 12.5,
    "width": 10.5,
    "height": 14,
    "location": "basement",
    "dateCreated": "2018-11-20 09:00:53"
}
```

This endpoint retrieves a specific enclosure.

### HTTP Request

`GET http://api.stepbystepml.io/agm/v1/enclosures/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the enclosure to retrieve

## Create Enclosures


> Example request

```json
{
    "enclosures": 
        {
            "title": "Basement Enclosure 1",
            "length": 12.5,
            "width": 10.5,
            "height": 14,
            "location": "basement"
        },
        {
            "title": "Basement Enclosure 2",
            "length": 12.5,
            "width": 10.5,
            "height": 14,
            "location": "basement"
        }
}
```

>Example response

```json
{
    "enclosures": 
        {
            "enclosureId": 12,
            "title": "Basement Enclosure 1",
            "length": 12.5,
            "width": 10.5,
            "height": 14,
            "location": "basement",
            "dateCreated": "2018-11-20 09:00:53"
        },
        {
            "enclosureId": 13,
            "title": "Basement Enclosure 2",
            "length": 12.5,
            "width": 10.5,
            "height": 14,
            "location": "basement",
            "dateCreated": "2018-12-20 09:00:53"
        }
}
```

Creates enclosure entities.

<aside class="notice"><code>enclosureId</code> and <code>dateCreated</code> are generated after entity creation, and can be found in the response body.</aside>

### HTTP Request

`POST http://api.stepbystepml.io/agm/v1/enclosures`

## Delete Enclosures

> Example request

```bash
$ curl http://api.stepbystepml.io/agm/v1/enclosures/12 \
   -u YOUR_API_KEY \
   -X DELETE
```

> Example response

```json
{
  "enclosureId": 12,
  "deleted": true
}
```
This endpoint deletes a specific enclosure.

<aside class="warning">Deleting enclosures is a permanent action and cannot be undone.</aside>


### HTTP Request

`DELETE http://api.stepbystepml.io/agm/v1/enclosures/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the enclosure to delete