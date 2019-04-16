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















# Enclosure Sensors

## Get All Enclosure Sensors

> Example response

```json
{
  "enclosure": [
    {
      "enclosure-id": 12,
      "enclosure-sensors": [
        {
          "sensor-id": 32,
          "type": "temperature-humidity",
          "location": "Near entrance",
          "date-created": "2018-11-20 09:00:53"
        },
        {
          "sensor-id": 33,
          "type": "temperature-humidity",
          "location": "Near exit",
          "date-created": "2018-11-20 09:00:53"
        }
      ],
      "plant-sensors": [
        {
          "plant-id": 5,
          "sensor-id": 8,
          "type": "soil-moisture",
          "date-created": "2018-11-20 09:00:53"
        },
        {
          "plant-id": 5,
          "sensor-id": 7,
          "type": "soil-moisture",
          "date-created": "2018-11-20 09:00:53"
        }
      ]
    },
    {
      "enclosure-id": 13,
      "enclosure-sensors": [
        {
          "sensor-id": 34,
          "type": "temperature-humidity",
          "date-created": "2018-11-20 09:00:53"
        },
        {
          "sensor-id": 35,
          "type": "temperature-humidity",
          "date-created": "2018-11-20 09:00:53"
        }
      ],
      "plant-sensors": [
        {
          "plant-id": 6,
          "sensor-id": 8,
          "type": "soil-temperature",
          "date-created": "2018-11-20 09:00:53"
        },
        {
          "plant-id": 7,
          "sensor-id": 7,
          "type": "temperature-humidity",
          "date-created": "2018-11-20 09:00:53"
        }
      ]
    }
  ]
}
```
Retrieves all the sensors from all the enclosures associated with your account.
<aside class="warning">
<code>sensor-id</code> is NOT unique for the set of all sensors, but rather each <code>sensor-id</code> is unique for each sensor type. 
</aside>
<aside class="notice">
The <code>enclosure-sensors</code> array are the sensors that read enclosure data (i.e. temperature and humidity). The <code>plant-sensors</code> array are the plant sensors of each plant within the given enclosure.
</aside>

### HTTP Request

`GET http://api.stepbystepml.io/agm/v1/sensors/enclosure`

## Get the sensors present within a specific enclosure

> Example request

```bash
$ curl http://api.stepbystepml.io/agm/v1/sensors/enclosure/28 \
   -u YOUR_API_KEY \
   -X GET
```

> Example response

```json
{
        "enclosure-id": 28,
        "enclosure-sensors": [
            {
                "sensor-id": 1,
                "type": "temperature-humidity",
                "location": "Middle of enclosure",
                "date-created": "2019-03-02T14:56:19.691+0000"
            },
            {
                "sensor-id": 1,
                "type": "temperature-humidity",
                "location": null,
                "date-created": "2019-03-02T14:56:19.691+0000"
            }
        ]
    }
```

This endpoint retrieves the sensors present within a specific enclosure. This includes both enclosure-sensors, and plant sensors.

### HTTP Request

`GET http://api.stepbystepml.io/agm/v1/sensors/enclosure/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the enclosure to retrieve sensor data from (not sensor readings)

## Create Enclosure Sensors

> Example request

```json
{
      "enclosure-sensors": [
        {
          "type": "temperature-humidity",
          "location": "Middle of enclosure"
        },
        {
          "type": "temperature-humidity"
        }
      ]
}
```

>Example response

```json
{
    "enclosure-id": 4,
    "enclosure-sensors": [
        {
            "sensor-id": 1,
            "type": "temperature-humidity",
            "location": "Middle of enclosure",
            "date-created": "2019-03-02T14:59:25.737+0000"
        },
        {
            "sensor-id": 1,
            "type": "temperature-humidity",
            "location": null,
            "date-created": "2019-03-02T14:59:25.737+0000"
        }
    ]
}
```

Creates sensor entities belonging to enclosure entities.

<aside class="notice">The <code>enclosure-id</code> must first exist before sensors can be added.</aside>

<aside class="notice">The <code>location</code> parameter only exists for enclosure sensors.</aside>

### HTTP Request

`POST http://api.stepbystepml.io/agm/v1/sensors/enclosure`

## Delete Enclosure Sensor

> Example request

```bash
$ curl http://api.stepbystepml.io/agm/v1/sensors/enclosure/35 \
   -u YOUR_API_KEY \
   -X DELETE
```

> Example response

```json
{
  "enclosure-id": 35,
  "deleted": true
}
```
This endpoint deletes a specific enclosure sensor.

<aside class="warning">Deleting an enclosure sensor is a permanent action and cannot be undone.</aside>


### HTTP Request

`DELETE http://api.stepbystepml.io/agm/v1/sensors/enclosure/<sensor-type>/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The sensor ID to be deleted
sensor-type | The type of sensor to be deleted (<code>temperature-humidity</code>)

# Plant Sensors

## Get All Plant Sensors

> Example response

```json
{
  "plant": [
    {
      "plant-id": 12,
      "plant-sensors": [
        {
          "sensor-id": 8,
          "type": "soil-moisture",
          "date-created": "2018-11-20 09:00:53"
        },
        {
          "sensor-id": 7,
          "type": "soil-moisture",
          "date-created": "2018-11-20 09:00:53"
        }
      ]
    },
    {
      "plant-id": 13,
      "plant-sensors": [
        {
          "sensor-id": 8,
          "type": "soil-temperature",
          "date-created": "2018-11-20 09:00:53"
        },
        {
          "sensor-id": 7,
          "type": "temperature-humidity",
          "date-created": "2018-11-20 09:00:53"
        }
      ]
    }
  ]
}
```
Retrieves all the sensors from all the plants associated with your account.
<aside class="warning">
<code>sensor-id</code> is NOT unique for the set of all sensors, but rather each <code>sensor-id</code> is unique for each sensor type. 
</aside>

### HTTP Request

`GET http://api.stepbystepml.io/agm/v1/sensors/plant`

## Get the sensors present for a specific plant

> Example request

```bash
$ curl http://api.stepbystepml.io/agm/v1/sensors/plant/13 \
   -u YOUR_API_KEY \
   -X GET
```

> Example response

```json
{
  "plant": [
    {
      "plant-id": 13,
      "plant-sensors": [
        {
          "sensor-id": 8,
          "type": "soil-temperature",
          "date-created": "2018-11-20 09:00:53"
        },
        {
          "sensor-id": 7,
          "type": "temperature-humidity",
          "date-created": "2018-11-20 09:00:53"
        }
      ]
    }
  ]
}
```

This endpoint retrieves the sensors present for a specific plant.

### HTTP Request

`GET http://api.stepbystepml.io/agm/v1/sensors/plant/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the plant to retrieve sensor data from (not sensor readings)

## Create Plant Sensors

> Example request

```json
{
  "plant": [
    {
      "plant-id": 28,
      "plant-sensors": [
        {
          "type": "soil-moisture",
        },
        {
          "type": "temperature-humidity"
        },
        ,
        {
          "type": "soil-temperature"
        }
      ]
    },
    {
      "plant-id": 29,
      "plant-sensors": [
        {
          "type": "soil-moisture",
        },
        {
          "type": "soil-moisture",
        }
      ]
    }
  ]
}
```

>Example response

```json
{
  "plant": [
    {
      "plant-id": 28,
      "plant-sensors": [
        {
          "sensor-id": 8,
          "type": "soil-moisture",
          "date-created": "2018-11-20 09:00:53"
        },
        {
          "sensor-id": 17,
          "type": "temperature-humidity",
          "date-created": "2018-11-20 09:00:53"
        },
        {
          "sensor-id": 28,
          "type": "soil-temperature",
          "date-created": "2018-11-20 09:00:53"
        }
      ]
    },
    {
      "plant-id": 29,
      "plant-sensors": [
        {
          "sensor-id": 9,
          "type": "soil-moisture",
          "date-created": "2018-11-20 09:00:53"
        },
        {
          "sensor-id": 10,
          "type": "soil-moisture",
          "date-created": "2018-11-20 09:00:53"
        }
      ]
    }
  ]
}
```

Creates sensor entities belonging to plant entities.

<aside class="notice">The <code>plant-id</code> must first exist before sensors can be added.</aside>

### HTTP Request

`POST http://api.stepbystepml.io/agm/v1/sensors/plant`

## Delete Plant Sensor

> Example request

```bash
$ curl http://api.stepbystepml.io/agm/v1/sensors/plant/soil-moisture/8 \
   -u YOUR_API_KEY \
   -X DELETE
```

> Example response

```json
{
  "type": "soil-moisture",
  "sensor-id": 8,
  "deleted": true
}
```
This endpoint deletes a specific enclosure sensor.

<aside class="warning">Deleting an enclosure sensor is a permanent action and cannot be undone.</aside>


### HTTP Request

`DELETE http://api.stepbystepml.io/agm/v1/sensors/enclosure/<sensor-type>/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The sensor ID to be deleted
sensor-type | The type of sensor to be deleted (one of <code>temperature-humidity</code>, <code>soil-moisture</code>, or <code>soil-temperature</code>)


# Enclosures

## Get All Enclosures

> Example response

```json
{
    "enclosures": [
        {
            "enclosure-id": 12,
            "title": "Basement Enclosure 1",
            "length": 12.5,
            "width": 10.5,
            "height": 14,
            "location": "basement",
            "date-created": "2018-11-20 09:00:53"
        },
        {
            "enclosure-id": 13,
            "title": "Basement Enclosure 2",
            "length": 12.5,
            "width": 10.5,
            "height": 14,
            "location": "basement",
            "date-created": "2018-12-20 09:00:53"
        }
    ]
}
```

Lists all enclosures associated with your account.

### HTTP Request

`GET http://api.stepbystepml.io/agm/v1/sensors`

## Get a Specific Enclosure

> Example request
```bash
$ curl http://api.stepbystepml.io/agm/v1/enclosures/12 \
   -u YOUR_API_KEY \
   -X GET
```

> Example response

```json
{
    "enclosure-id": 12,
    "title": "Basement Enclosure 1",
    "length": 12.5,
    "width": 10.5,
    "height": 14,
    "location": "basement",
    "date-created": "2018-11-20 09:00:53"
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
    "enclosures": [
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
    ]
}
```

>Example response

```json
{
    "enclosures": [
        {
            "enclosure-id": 12,
            "title": "Basement Enclosure 1",
            "length": 12.5,
            "width": 10.5,
            "height": 14,
            "location": "basement",
            "date-created": "2018-11-20 09:00:53"
        },
        {
            "enclosure-id": 13,
            "title": "Basement Enclosure 2",
            "length": 12.5,
            "width": 10.5,
            "height": 14,
            "location": "basement",
            "date-created": "2018-12-20 09:00:53"
        }
    ]
}
```

Creates enclosure entities.

<aside class="notice"><code>enclosure-id</code> and <code>date-created</code> are generated after entity creation, and can be found in the response body.</aside>

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
  "enclosure-id": 12,
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


# Readings

## Get All Readings

> Example response for /readings/soil-moisture

```json
{
  "readings": [
    {
      "sensor-reading-id": 84839,
      "sensor-id": 13,
      "moisture-level": 12,
      "moisture-level-units": "percent",
      "time-recorded": "2018-11-20 08:52:53",
      "date-created": "2018-11-20 09:00:53"
    },
    {
      "sensor-reading-id": 84840,
      "sensor-id": 13,
      "moisture-level": 12.2,
      "moisture-level-units": "percent",
      "time-recorded": "2018-11-20 08:52:53",
      "date-created": "2018-11-20 09:00:53"
    }
  ]
}
```

> Example response for /readings/soil-temperature

```json
{
  "readings": [
    {
      "sensor-reading-id": 53394,
      "sensor-id": 9,
      "temp-level": 43,
      "temp-scale": "f",
      "time-recorded": "2018-11-20 08:52:53",
      "date-created": "2018-11-20 09:00:53"
    },
    {
      "sensor-reading-id": 53395,
      "sensor-id": 12,
      "temp-level": 43.2,
      "temp-scale": "f",
      "time-recorded": "2018-11-20 08:52:53",
      "date-created": "2018-11-20 09:00:53"
    }
  ]
}
```

> Example response for /readings/temperature-humidity

```json
{
  "readings": [
    {
      "sensor-reading-id": 223,
      "sensor-id": 84,
      "temp-level": 22,
      "temp-scale": "c",
      "humidity": 44.5,
      "humidity-units": "percent",
      "time-recorded": "2018-11-20 08:52:53",
      "date-created": "2018-11-20 09:00:53"
    },
    {
      "sensor-reading-id": 224,
      "sensor-id": 82,
      "temp-level": 22.3,
      "temp-scale": "c",
      "humidity": 44.5,
      "humidity-units": "percent",
      "time-recorded": "2018-11-20 08:52:53",
      "date-created": "2018-11-20 09:00:53"
    }
  ]
}
```

Retrieves all the readings for the passed sensor type. Results are paged.

### HTTP Request

`GET http://api.stepbystepml.io/agm/v1/readings/<sensor-type>`

Parameter | Description
--------- | -----------
sensor-type | <code>temperature-humidity</code>, <code>soil-moisture</code>, or <code>soil-temperature</code>

Query Parameter | Description
--------- | -----------
limit | The limit for the query
offset | The offset

### Query Parameter Example
<code>http://api.stepbystepml.io/agm/v1/readings/soil-moisture?limit=20&offset=40</code>: This would return the next 20 rows starting with the 40th row.


## Get readings from a specific sensor

> Example request

```bash
$ curl http://api.stepbystepml.io/agm/v1/readings/temperature-humidity/84 \
   -u YOUR_API_KEY \
   -X GET
```

> Example response

```json
{
  "readings": [
    {
      "sensor-reading-id": 223,
      "sensor-id": 84,
      "temp-level": 22,
      "temp-scale": "c",
      "humidity": 44.5,
      "humidity-units": "percent",
      "time-recorded": "2018-11-20 08:52:53",
      "date-created": "2018-11-20 09:00:53"
    },
    {
      "sensor-reading-id": 224,
      "sensor-id": 84,
      "temp-level": 22.3,
      "temp-scale": "c",
      "humidity": 44.5,
      "humidity-units": "percent",
      "time-recorded": "2018-11-20 08:52:53",
      "date-created": "2018-11-20 09:00:53"
    }
  ]
}
```

Retrieves the sensor readings from the specified <code>sensor-type</code> - <code>sensor-id</code> combination

`GET http://api.stepbystepml.io/agm/v1/readings/<sensor-type>/<sensor-id>`

Parameter | Description
--------- | -----------
sensor-type | <code>temperature-humidity</code>, <code>soil-moisture</code>, or <code>soil-temperature</code>
sensor-id | The <code>sensor-id</code> of the sensor to retrieve the readings from.

Query Parameter | Description
--------- | -----------
limit | The limit for the query
offset | The offset

### Query Parameter Example
<code>http://api.stepbystepml.io/agm/v1/readings/soil-moisture?limit=20&offset=40</code>: This would return the next 20 rows starting with the 40th row.


## Create Sensor Reading

> Example request for <code>soil-moisture</code> sensor
> <code>POST /agm/v1/readings/soil-moisture</code>

```json
{
  "readings": [
    {
      "sensor-id": 23,
      "moisture-level": 21,
      "moisture-level-units": "percent",
      "time-recorded": "2018-11-20 03:00:53"
    },
    {
      "sensor-id": 22,
      "moisture-level": 21,
      "moisture-level-units": "percent",
      "time-recorded": "2018-11-20 03:00:53"
    }
  ]
}
```

>Example response for <code>soil-moisture</code> sensor

```json
{
  "readings": [
    {
      "reading-id": 98327,
      "sensor-id": 23,
      "moisture-level": 21,
      "moisture-level-units": "percent",
      "time-recorded": "2018-11-20 03:00:53",
      "date-created": "2018-11-20 03:00:53"
    },
    {
      "reading-id": 98328,
      "sensor-id": 22,
      "moisture-level": 21,
      "moisture-level-units": "percent",
      "time-recorded": "2018-11-20 03:00:53",
      "date-created": "2018-11-20 03:00:53"
    }
  ]
}
```

> Example request for <code>soil-temperature</code> sensor
> <code>POST /agm/v1/readings/soil-temperature</code>

```json
{
  "readings": [
    {
      "sensor-id": 211,
      "temperature-level": 74.3,
      "temperature-scale": "f",
      "time-recorded": "2018-11-20 03:00:53"
    },
    {
      "sensor-id": 211,
      "temperature-level": 23.2,
      "temperature-scale": "c",
      "time-recorded": "2018-11-20 03:00:53"
    }
  ]
}
```

>Example response for <code>soil-temperature</code> sensor

```json
{
  "readings": [
    {
      "reading-id": 98347,
      "sensor-id": 211,
      "temperature-level": 74.3,
      "temperature-scale": "f",
      "time-recorded": "2018-11-20 03:00:53",
      "date-created": "2018-11-20 03:00:53"
    },
    {
      "reading-id": 98348,
      "sensor-id": 211,
      "temperature-level": 23.2,
      "temperature-scale": "c",
      "time-recorded": "2018-11-20 03:00:53",
      "date-created": "2018-11-20 03:00:53"
    }
  ]
}
```

> Example request for <code>temperature-humidity</code> sensor
> <code>POST /agm/v1/readings/temperature-humidity</code>

```json
{
  "readings": [
    {
      "sensor-id": 77,
      "temperature-level": 23.2,
      "temperature-scale": "c",
      "moisture-level-units": "percent",
      "time-recorded": "2018-11-20 03:00:53"
    },
    {
      "sensor-id": 78,
      "moisture-level": 21,
      "temperature-level": 73,
      "temperature-scale": "f",
      "moisture-level-units": "percent",
      "time-recorded": "2018-11-20 03:00:53"
    }
  ]
}
```

>Example response for <code>temperature-humidity</code> sensor

```json
{
  "readings": [
    {
      "sensor-reading-id": 7738,
      "sensor-id": 77,
      "temperature-level": 23.2,
      "temperature-scale": "c",
      "moisture-level-units": "percent",
      "time-recorded": "2018-11-20 03:00:53",
      "date-created": "2018-11-20 03:00:53"
    },
    {
      "sensor-reading-id": 7739,
      "sensor-id": 78,
      "moisture-level": 21,
      "temperature-level": 73,
      "temperature-scale": "f",
      "moisture-level-units": "percent",
      "time-recorded": "2018-11-20 03:00:53",
      "date-created": "2018-11-20 03:00:53"
    }
  ]
}
```

Creates sensor readings for the specified sensor type.

<aside class="notice">For each reading, the associated sensor-id must exist. For instance, to add readings to <code>/readings/soil-moisture</code>, <code>sensor-id</code> must first exist before sensor readings can be added.</aside>


### HTTP Request

`POST http://api.stepbystepml.io/agm/v1/readings/<sensor-type>`

Parameter | Description
--------- | -----------
sensor-type | <code>temperature-humidity</code>, <code>soil-moisture</code>, or <code>soil-temperature</code>



## Delete Sensor Reading

> Example request

```bash
$ curl http://api.stepbystepml.io/agm/v1/readings/temperature-humidity/7739 \
   -u YOUR_API_KEY \
   -X DELETE
```

> Example response

```json
{
  "type": "temperature-humidity",
  "sensor-id": 78,
  "sensor-reading-id": 7739,
  "deleted": true
}
```
This endpoint deletes a specific sensor reading, according to the passed <code>sensor-type</code>.


### HTTP Request

`DELETE http://api.stepbystepml.io/agm/v1/sensors/enclosure/<sensor-type>/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The reading ID to be deleted
sensor-type | The type of sensor to be deleted (<code>temperature-humidity</code>)
