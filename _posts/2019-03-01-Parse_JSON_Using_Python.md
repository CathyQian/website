---
layout: post
title: Parse JSON Using Python
date: 2019-03-01
comments: true
---

Using weather API to deploy a HTTP GET call: https://api.weather.gov/gridpoints/TOP/31,80 in Postman, we will get the following JSON file as a return.

So how do we extract useful information from the JSON file?

```python
data = [{"context": 
        ["https://raw.githubusercontent.com/geojson/geojson-ld/master/contexts/geojson-base.jsonld",
        {
            "wx": "https://api.weather.gov/ontology#",
            "s": "https://schema.org/",
            "geo": "http://www.opengis.net/ont/geosparql#",
            "unit": "http://codes.wmo.int/common/unit/",
            "@vocab": "https://api.weather.gov/ontology#",
            "geometry": {
                "@id": "s:GeoCoordinates",
                "@type": "geo:wktLiteral"
            },
            "city": "s:addressLocality",
            "state": "s:addressRegion",
            "distance": {
                "@id": "s:Distance",
                "@type": "s:QuantitativeValue"
            }
        }
    ],
    "id": "https://api.weather.gov/gridpoints/TOP/31,80",
    "type": "Feature",
    "geometry": {
        "type": "Polygon",
        "coordinates": [
            [
                [
                    -97.1089731,
                    39.766826299999998
                ]
            ]
        ]
    },
    "properties": {
        "@id": "https://api.weather.gov/gridpoints/TOP/31,80",
        "@type": "wx:Gridpoint",
        "updateTime": "2018-11-07T17:10:41+00:00",
        "validTimes": "2018-11-07T11:00:00+00:00/P7DT14H",
        "elevation": {
            "value": 441.96000000000004,
            "unitCode": "unit:m"
        },
        "forecastOffice": "https://api.weather.gov/offices/TOP",
        "gridId": "TOP",
        "gridX": "31",
        "gridY": "80",
        "temperature": {
            "sourceUnit": "F",
            "uom": "unit:degC",
            "values": [
                {
                    "validTime": "2018-11-07T13:00:00+00:00/PT2H",
                    "value": -1.6666666666666288
                }]
        }
    }
}]
```

```python
import json

# Serialize obj to a JSON formatted str
json_string = json.dumps(data)
type(json_string)

# store data into a json file
with open('data.json', 'w') as outfile:
    json.dump(data, outfile)

# load json string into data
data = json.loads(json_string)
type(data)

# retrieve data as a dictionary
data[0]["context"][1]["wx"]

```

# References:
1. https://developer.rhino3d.com/guides/rhinopython/python-xml-json/
2. https://docs.python.org/3.7/library/json.html#py-to-json-table
