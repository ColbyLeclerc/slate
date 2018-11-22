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

# Sensors

## Get All Sensors

> Example response

```json
{
  "enclosures": [
    {
      "sensor-id": 12,
      "type": "temperature-humidity",
      "enclosure-id": 86
    },
    {
      "sensor-id": 13,
      "type": "temperature-humidity",
      "enclosure-id": 86
    },
    {
      "sensor-id": 18,
      "type": "temperature-humidity",
      "enclosure-id": 98
    },
  ],
  "plants": [
    {
      "sensor-id": 33,
      "type": "soil-moisture",
      "plant-id": 222
    },
    {
      "plant-sensor-id": 34,
      "type": "soil-moisture",
      "plant-id": 222
    },
    {
      "plant-sensor-id": 44,
      "type": "soil-temperature",
      "plant-id": 223
    },
  ]
}
```

This endpoint returns all sensor types and their respected ids. To perform other CRUD operations, see <code>/sensors/enclosure</code> listed under Enclosure Sensors and <code>/sensors/plant</code> listed under Plant Sensors.

### HTTP Request

`GET http://api.stepbystepml.io/agm/v1/sensors`

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
  "enclosure": [
    {
      "enclosure-id": 28,
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
  "enclosure": [
    {
      "enclosure-id": 28,
      "enclosure-sensors": [
        {
          "type": "temperature-humidity",
          "location": "Middle of enclosure"
        },
        {
          "type": "temperature-humidity"
        }
      ]
    },
    {
      "enclosure-id": 29,
      "enclosure-sensors": [
        {
          "type": "temperature-humidity"
        }
      ]
    }
  ]
}
```

>Example response

```json
{
  "enclosure": [
    {
      "enclosure-id": 28,
      "enclosure-sensors": [
        {
          "sensor-id": 32,
          "type": "temperature-humidity",
          "location": "Near entrance",
          "date-created": "2018-11-20 09:00:53"
        },
        {
          "sensor-id": 34,
          "type": "temperature-humidity",
          "date-created": "2018-11-20 09:00:53"
        }
      ]
    },
    {
      "enclosure-id": 29,
      "enclosure-sensors": [
        {
          "sensor-id": 35,
          "type": "temperature-humidity",
          "date-created": "2018-11-20 09:00:53"
        }
      ]
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
$ curl http://api.stepbystepml.io/agm/v1/sensors/enclosure/temperature-humidity/35 \
   -u YOUR_API_KEY \
   -X DELETE
```

> Example response

```json
{
  "type": "temperature-humidity",
  "sensor-id": 35,
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
