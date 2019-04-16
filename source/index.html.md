---
title: Advanced Garden Monitor API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - json

toc_footers:
  #- <a href='#'>Sign Up for a Developer Key</a>
  #- <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

includes:
#  - errors

search: true
---

# Introduction

The Advanced Garden Monitor (AGM) API allows users to create, retrieve, and delete objects such as sensors, enclosures, plants, and sensor readings. 

This REST API uses CRUD operations to send requests to the specified endpoints. Each endpoint also supports pagnation.

# Authentication

> To authorize, use this code:


> Make sure to replace `YOUR_API_KEY` with your API key.

AGM uses API keys to allow access to the API. You can register a new AGM API key at our [developer portal](http://key.agm-api.com).

AGM expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: YOUR_API_KEY`

<aside class="notice">
You must replace <code>YOUR_API_KEY</code> with your personal API key.
</aside>

## Get Auth Record

> Example response

```json
{
    "auth-id": 1,
    "token": "18e19745-5555-4f94-9a5f-6cde383797dd",
    "email-addr": "test.email@agm-api.com",
    "create-timestamp": "2019-03-24T10:58:05.242",
    "update-timestamp": "2019-03-24T10:58:05.243"
}
```

Retrieve an auth record.
<aside class="notice">This is here for documentation purposes, however in production this endpoint will be restricted to internal requests only, thus blocked from the outside world.</aside>

### HTTP Request

`GET https://agm-api.com/agm/v1/auth/12`

## Create Auth Record

> Example request

```json
{
  "first-name": "jasper",
  "last-name": "smith",
  "email-addr": "test.email@agm-api.com"
}
```

>Example response

```json
{
  "token":"156c6930-555-47e7-9792-ddf4f344c749",
  "first-name": "jasper",
  "last-name": "smith",
  "email-addr": "test.email@agm-api.com",
  "create-timestamp": "2019-03-24T10:58:05.242",
  "update-timestamp": "2019-03-24T10:58:05.243"
}
```

Creates auth entity.

<aside class="notice">Currently, no fields are required. The associated email address, and password hash/salt combination will be required in production. Further, in production the <code>password-hash</code> and <code>salt</code> will be available for internal calls.</aside>

### HTTP Request

`POST https://agm-api.com/agm/v1/enclosures`

# Enclosure

## Get All Enclosures

> Example response

```json
[
    {
        "title": "Succulents",
        "location": "Attic",
        "length": 12,
        "width": 12,
        "height": 12,
        "plants": [
            {
                "name": "Succulent 1",
                "yield": 0,
                "plant-id": 1,
                "enclosure-id": 1,
                "pot-size": 12,
                "pot-size-units": "gallons",
                "created-date-time": "2019-04-16T12:47:20.307",
                "last-updated-date-time": "2019-04-16T12:47:20.307"
            }
        ],
        "sensors": [
            {
                "enclosure": true,
                "plant": false,
                "sensor-id": 2,
                "plant-id": 1,
                "enclosure-id": 1,
                "sensor-type": "temperature-humidity",
                "is-plant": false,
                "is-enclosure": true,
                "created-date-time": "2019-04-16T13:24:03.077",
                "last-updated-date-time": "2019-04-16T13:24:03.077"
            }
        ],
        "enclosure-id": 1,
        "dimension-units": "meters",
        "created-date-time": "2019-04-16T12:47:10.705",
        "last-updated-date-time": "2019-04-16T12:47:10.705"
    },
    {
        "title": "Peppers",
        "location": "Attic (Right Size)",
        "length": 12,
        "width": 12,
        "height": 12,
        "plants": [
            {
                "name": "Succulent 1",
                "yield": 0,
                "plant-id": 1,
                "enclosure-id": 1,
                "pot-size": 12,
                "pot-size-units": "gallons",
                "created-date-time": "2019-04-16T12:47:20.307",
                "last-updated-date-time": "2019-04-16T12:47:20.307"
            }
        ],
        "sensors": [],
        "enclosure-id": 1,
        "dimension-units": "meters",
        "created-date-time": "2019-04-16T12:47:10.705",
        "last-updated-date-time": "2019-04-16T12:47:10.705"
    }
]
```

<aside class="notice">This endpoint not only returns enclosure details, but also the sensors, and plants associated with the enclosure. This is done to allow for fewer requests for the UI, in exchange for duplicate info being presented across the endpoint schema.</aside>

## Get Single Enclosure

> Example response

```json
{
   "title":"Succulents",
   "location":"Attic",
   "length":12,
   "width":12,
   "height":12,
   "plants":[
      {
         "name":"Succulent 1",
         "yield":0,
         "plant-id":1,
         "enclosure-id":1,
         "pot-size":12,
         "pot-size-units":"gallons",
         "created-date-time":"2019-04-16T12:47:20.307",
         "last-updated-date-time":"2019-04-16T12:47:20.307"
      }
   ],
   "sensors":[
      {
         "enclosure":true,
         "plant":false,
         "sensor-id":2,
         "plant-id":1,
         "enclosure-id":1,
         "sensor-type":"temperature-humidity",
         "is-plant":false,
         "is-enclosure":true,
         "created-date-time":"2019-04-16T13:24:03.077",
         "last-updated-date-time":"2019-04-16T13:24:03.077"
      }
   ],
   "enclosure-id":1,
   "dimension-units":"meters",
   "created-date-time":"2019-04-16T12:47:10.705",
   "last-updated-date-time":"2019-04-16T12:47:10.705"
}
```

<aside class="notice">This endpoint returns all sensors assocaited with the account. Note there exists a difference between enclosure sensors, and plant sensors, as defined by the <code>is-plant</code> and <code>is-enclosure</code> fields.</aside>


### HTTP Request

`GET https://agm-api.com/agm/v1/enclosures/1`

## Create Enclosure

> Example request

```json
{
    "title": "Succulents",
    "location": "Attic",
    "length": 2,
    "dimension-units": "meters",
    "width": 3,
    "height": 4
}
```

>Example response

```json
{
    "title": "Succulents",
    "location": "Attic",
    "length": 2,
    "width": 3,
    "height": 4,
    "plants": [],
    "sensors": [],
    "enclosure-id": 2,
    "dimension-units": "meters",
    "created-date-time": "2019-04-16T13:45:07.02",
    "last-updated-date-time": "2019-04-16T13:45:07.02"
}
```

Creates an enclosure entity.

<aside class="notice">Note the <code>plants</code> and <code>sensor</code> arrays are empty. This is because there does not exist any associated plants nor sesnors.</aside>

### HTTP Request

`POST https://agm-api.com/agm/v1/enclosures`

## Delete Single Enclosure

> Example response

```json
{
    "message": "enclosure deleted successfully",
    "deleted": "true",
    "enclosure-id": 1
}
```

Deletes an enclosure entity

### HTTP Request

`DELETE https://agm-api.com/agm/v1/enclosures/1`

# Plants

## Get All Plants

> Example response

```json
[
    {
        "name": "Cactus 1",
        "yield": 0,
        "plant-id": 2,
        "enclosure-id": 1,
        "pot-size": 5,
        "pot-size-units": "gallons",
        "created-date-time": "2019-04-16T14:04:13.142",
        "last-updated-date-time": "2019-04-16T14:04:13.142"
    },
    {
        "name": "Cactus 2",
        "yield": 0,
        "plant-id": 3,
        "enclosure-id": 1,
        "pot-size": 5,
        "pot-size-units": "gallons",
        "date-planted": "2019-04-14T14:04:13.142",
        "created-date-time": "2019-04-16T14:04:58.175",
        "last-updated-date-time": "2019-04-16T14:04:58.175"
    }
]
```

This endpoint returns all plants assocaited with the account.

<aside class="notice">If there exist any associated plants or sensors with the enclosure, the delete request will be rejected (due to there being existing dependencies). In such a case, you must first delete the entities that depend on the enclosure beforehand.</aside>

### HTTP Request

`GET https://agm-api.com/agm/v1/plants`

## Get Single Plant

> Example response

```json
{
    "name": "Cactus 2",
    "yield": 0,
    "plant-id": 3,
    "enclosure-id": 1,
    "pot-size": 5,
    "pot-size-units": "gallons",
    "date-planted": "2019-04-14T14:04:13.142",
    "created-date-time": "2019-04-16T14:04:58.175",
    "last-updated-date-time": "2019-04-16T14:04:58.175"
}
```

Returns the associated plant entity.


### HTTP Request

`GET https://agm-api.com/agm/v1/plants/3`

## Create Plant

> Example request

```json
{
  "name": "Cactus 2",
	"pot-size": 5,
	"pot-size-units": "gallons",
	"yield": 0,
	"enclosure-id": 1,
	"date-planted": "2019-04-14T14:04:13.142",
	"date-harvested": ""
}
```

>Example response

```json
{
    "name": "Cactus 2",
    "yield": 0,
    "plant-id": 3,
    "enclosure-id": 1,
    "pot-size": 5,
    "pot-size-units": "gallons",
    "date-planted": "2019-04-14T14:04:13.142",
    "created-date-time": "2019-04-16T14:04:58.175",
    "last-updated-date-time": "2019-04-16T14:04:58.175"
}
```

Creates a plant entity.

<aside class="notice">The <code>date-planted</code>, <code>date-harvested</code>, and <code>yield</code> fields are not required. </aside>

### HTTP Request

`POST https://agm-api.com/agm/v1/plants`

## Delete Single Plant

> Example response

```json
{
    "message": "plant deleted successfully",
    "deleted": "true",
    "plant-id": 3
}
```

Deletes a sensor entity

### HTTP Request

`DELETE https://agm-api.com/agm/v1/plants/3`

# Sensors

## Get All Sensors

> Example response

```json
[
  {
        "sensor-id": 150,
        "plant-id": 49,
        "enclosure-id": 53,
        "sensor-type": "temperature-humidity",
        "is-plant": false,
        "is-enclosure": true,
        "created-date-time": "2019-04-15T11:43:16.054",
        "last-updated-date-time": "2019-04-15T11:43:16.054"
  },
  {
        "sensor-id": 151,
        "plant-id": 49,
        "enclosure-id": 53,
        "sensor-type": "soil-temperature",
        "is-plant": true,
        "is-enclosure": false,
        "created-date-time": "2019-04-15T11:43:27.215",
        "last-updated-date-time": "2019-04-15T11:43:27.215"
  }
]
```

This endpoint returns all sensors assocaited with the account. Note there exists a difference between enclosure sensors, and plant sensors, as defined by the <code>is-plant</code> and <code>is-enclosure</code> fields.

### HTTP Request

`GET https://agm-api.com/agm/v1/sensors`

## Get Single Sensor

> Example response

```json
{
    "sensor-id": 1,
    "plant-id": 45,
    "enclosure-id": 1,
    "sensor-type": "temperature-humidity",
    "is-plant": false,
    "is-enclosure": true,
    "created-date-time": "2019-04-16T12:47:27.963",
    "last-updated-date-time": "2019-04-16T12:47:27.963"
}
```

This endpoint returns all sensors assocaited with the account. Note there exists a difference between enclosure sensors, and plant sensors, as defined by the <code>is-plant</code> and <code>is-enclosure</code> fields.


### HTTP Request

`GET https://agm-api.com/agm/v1/sensors/1`

## Create Sensor

> Example request

```json
{
 	"plant-id": 1,
  "enclosure-id": 1,
  "is-enclosure": false,
  "is-plant": true,
  "sensor-type": "soil-moisture"
}
```

>Example response

```json
{
    "sensor-id": 1,
    "plant-id": 1,
    "enclosure-id": 1,
    "sensor-type": "soil-moisture",
    "is-plant": true,
    "is-enclosure": false,
    "created-date-time": "2019-04-16T12:47:27.963",
    "last-updated-date-time": "2019-04-16T12:47:27.963"
}
```

Creates a sensor entity.

<aside class="notice">The <code>enclosure-id</code> field is not required, as a plant can only be associated with a single enclosure. Thus, if the <code>enclosure-id</code> is not provided, a lookup is performed to populate this field.</aside>

### HTTP Request

`POST https://agm-api.com/agm/v1/sensors`

## Delete Single Sensor

> Example response

```json
{
    "message": "sensor deleted successfully",
    "deleted": "true",
    "sensor-id": 1
}
```

Deletes a sensor entity

### HTTP Request

`DELETE https://agm-api.com/agm/v1/sensors/1`


# Readings

## Get All <code>temperature-humidity</code> Readings

> Example response

```json
[
  {
    "temperature-humidity-id": 1,
    "sensor-id": 1,
    "temp-level": 76,
    "temp-scale": "f",
    "humidity": 12.4,
  	"humidity-units": "percent",
    "time-recorded": "2019-04-14T14:04:14.844",
    "created-date-time": "2019-04-16T14:13:39.779",
    "last-updated-date-time": "2019-04-16T14:13:39.779"
  },
  {
    "temperature-humidity-id": 2,
    "sensor-id": 2,
    "temp-level": 74,
    "temp-scale": "f",
    "humidity": 12.4,
	  "humidity-units": "percent",
    "time-recorded": "2019-04-14T14:05:15.844",
    "created-date-time": "2019-04-16T14:13:39.779",
    "last-updated-date-time": "2019-04-16T14:13:39.779"
  }
]
```

This endpoint returns all <code>temperature-humidity</code> readings associated with the account

### HTTP Request

`GET https://agm-api.com/agm/v1/readings/temperature-humidity`


## Get Single <code>temperature-humidity</code> Reading

> Example response

```json
{
    "temperature-humidity-id": 1,
    "sensor-id": 1,
    "temp-level": 76,
    "temp-scale": "f",
    "humidity": 12.4,
	  "humidity-units": "percent",
    "time-recorded": "2019-04-14T14:04:14.844",
    "created-date-time": "2019-04-16T14:13:39.779",
    "last-updated-date-time": "2019-04-16T14:13:39.779"
}
```

Returns the <code>temperature-humidity</code> reading associated with the id


### HTTP Request

`GET https://agm-api.com/agm/v1/readings/temperature-humidity/1`

## Create <code>temperature-humidity</code> Reading

> Example request

```json
{
  "sensor-id": 1,
	"temp-level": 76,
	"temp-scale": "f",
	"humidity": 12.4,
	"humidity-units": "percent",
	"time-recorded": "2019-04-14T14:04:14.844"
}
```

>Example response

```json
{
    "temperature-humidity-id": 1,
    "sensor-id": 2,
    "temp-level": 76,
    "temp-scale": "f",
    "humidity": 12.4,
  	"humidity-units": "percent",
    "time-recorded": "2019-04-14T14:04:14.844",
    "created-date-time": "2019-04-16T14:13:39.779",
    "last-updated-date-time": "2019-04-16T14:13:39.779"
}
```

Creates a <code>temperature-humidity</code> reading.
### HTTP Request

`POST https://agm-api.com/agm/v1/readings/temperature-humidity`

## Delete Single <code>temperature-humidity</code> Reading

> Example response

```json
{
    "message": "reading deleted successfully",
    "deleted": "true",
    "temperature-humidity-id": 1
}
```

Deletes a temperature-humidity reading entity

### HTTP Request

`DELETE https://agm-api.com/agm/v1/readings/temperature-humidity/1`



## Get All <code>soil-moisture</code> Readings

> Example response

```json
[
  {
    "soil-moisture-reading-id": 3,
    "sensor-id": 1,
    "moisture-level": 18.2,
    "moisture-level-units": "percent",
    "time-recorded": "2019-04-14T14:04:14.844",
    "created-date-time": "2019-04-16T14:23:49.449",
    "last-updated-date-time": "2019-04-16T14:23:49.449"
  },
  {
    "soil-moisture-reading-id": 4,
    "sensor-id": 1,
    "moisture-level": 18.2,
    "moisture-level-units": "percent",
    "time-recorded": "2019-04-14T14:04:14.844",
    "created-date-time": "2019-04-16T14:23:49.449",
    "last-updated-date-time": "2019-04-16T14:23:49.449"
  }
]
```

This endpoint returns all <code>soil-moisture</code> readings associated with the account

### HTTP Request

`GET https://agm-api.com/agm/v1/readings/soil-moisture`

## Get Single <code>soil-moisture</code> Reading

> Example response

```json
{
    "soil-moisture-reading-id": 3,
    "sensor-id": 1,
    "moisture-level": 18.2,
    "moisture-level-units": "percent",
    "time-recorded": "2019-04-14T14:04:14.844",
    "created-date-time": "2019-04-16T14:23:49.449",
    "last-updated-date-time": "2019-04-16T14:23:49.449"
}
```

Returns the <code>soil-moisture</code> reading associated with the id


### HTTP Request

`GET https://agm-api.com/agm/v1/readings/soil-moisture/1`

## Create <code>soil-moisture</code> Reading

> Example request

```json
{
	"sensor-id": 1,
	"moisture-level": 18.2,
	"moisture-level-units": "percent",
	"time-recorded": "2019-04-14T14:04:14.844"
}
```

>Example response

```json
{
    "soil-moisture-reading-id": 3,
    "sensor-id": 1,
    "moisture-level": 18.2,
    "moisture-level-units": "percent",
    "time-recorded": "2019-04-14T14:04:14.844",
    "created-date-time": "2019-04-16T14:23:49.449",
    "last-updated-date-time": "2019-04-16T14:23:49.449"
}
```

Creates a <code>soil-moisture</code> reading.
### HTTP Request

`POST https://agm-api.com/agm/v1/readings/soil-moisture`

## Delete Single <code>soil-moisture</code> Reading

> Example response

```json
{
    "message": "reading deleted successfully",
    "deleted": "true",
    "soil-moisture-reading-id": 1
}
```

Deletes a <code>soil-moisture</code> reading entity

### HTTP Request

`DELETE https://agm-api.com/agm/v1/readings/soil-moisture/1`

## Get All <code>soil-temperature</code> Readings

> Example response

```json
[
  {
   "soil-temperature-id": 2,
    "sensor-id": 0,
    "temp-level": 76,
    "temp-scale": "f",
    "time-recorded": "2019-04-14T14:04:14.84",
    "created-date-time": "2019-04-16T14:29:26.456",
    "last-updated-date-time": "2019-04-16T14:29:26.456"
  }
  {
     "soil-temperature-id": 3,
    "sensor-id": 0,
    "temp-level": 76,
    "temp-scale": "f",
    "time-recorded": "2019-04-14T14:04:14.84",
    "created-date-time": "2019-04-16T14:29:26.456",
    "last-updated-date-time": "2019-04-16T14:29:26.456"
  }
]
```

This endpoint returns all <code>soil-temperature</code> readings associated with the account

### HTTP Request

`GET https://agm-api.com/agm/v1/readings/soil-temperature`

## Get Single <code>soil-temperature</code> Reading

> Example response

```json
{
     "soil-temperature-id": 2,
    "sensor-id": 0,
    "temp-level": 76,
    "temp-scale": "f",
    "time-recorded": "2019-04-14T14:04:14.84",
    "created-date-time": "2019-04-16T14:29:26.456",
    "last-updated-date-time": "2019-04-16T14:29:26.456"
}
```

Returns the <code>soil-temperature</code> reading associated with the id


### HTTP Request

`GET https://agm-api.com/agm/v1/readings/soil-temperature/2`

## Create <code>soil-temperature</code> Reading

> Example request

```json
{
	"sensor-id": 1,
	"temp-level": 76,
	"temp-scale": "f",
	"time-recorded": "2019-04-14T14:04:14.84"
}
```

>Example response

```json
{
    "soil-temperature-id": 2,
    "sensor-id": 0,
    "temp-level": 76,
    "temp-scale": "f",
    "time-recorded": "2019-04-14T14:04:14.84",
    "created-date-time": "2019-04-16T14:29:26.456",
    "last-updated-date-time": "2019-04-16T14:29:26.456"
}
```

Creates a <code>temperature-humidity</code> reading.
### HTTP Request

`POST https://agm-api.com/agm/v1/readings/soil-temperature`

## Delete Single <code>soil-temperature</code> Reading

> Example response

```json
{
    "message": "reading deleted successfully",
    "deleted": "true",
    "soil-temperature-reading-id": 1
}
```

Deletes a sensor entity

### HTTP Request

`DELETE https://agm-api.com/agm/v1/readings/soil-temperature/1`