---
title: Indexer API Reference

language_tabs:
  - shell
  - python

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the ARM mbed Indexer API! You can use this API to get data about mbed
projects, create new projects in the indexer, or modify existing projects.

A "project" is simply a resource which describes where to find source code for
a program that is compatible with an ARM mbed enabled platform. The resource also
includes lots of other useful data which describes the project. This data can be
used by other services enabling features such as importing an mbed project into
a development environment, or looking up which projects are compatible with a
given mbed platform.

The API supports features such as pagination of results, and sorting & filtering
of results.

The API is designed to conform to the [JSON API spec](http://jsonapi.org), so both
server and client are obliged follow the specification in order to process valid
requests.


# The JSON API Content Type
All requests and responses which carry a JSON document must set the `Content-Type`
header to the JSON API content type to: `application/vnd.api+json`

Also the relevant `Accept` headers can be set in accordance with the spec.
Please see the section about [content negotiation](http://jsonapi.org/format/#content-negotiation-clients)
in the JSON API spec for more information on client responsibilities when handling JSON API requests/responses.


# Authentication
To do...


# Projects API

## Get

```python
import requests

response = requests.get("/projects/4ef62672-22aa-4eb7-92c3-dee8495fac4b")
```

```shell
curl -i "/projects/4ef62672-22aa-4eb7-92c3-dee8495fac4b"
```

> Below is an example of the data the above command may give:

```json
{
  "data": {
    "id": "4ef62672-22aa-4eb7-92c3-dee8495fac4b",
    "attributes": {
      "title": "Blinky",
      "branch_count": 3,
      "repo_owner": "ARM mbed",
      "license": "Apache 2.0",
      "fork_count": 1024,
      "provider": "GitHub",
      "url": "https://github.com/ARMmbed/example-mbedos-blinky",
      "imports": 5043,
      "protocol": "git",
      "summary": "Simple example program to blink an LED on an mbed board with mbed OS",
      "description": null,
      "follower_count": 3064,
      "version": "mbedos-16.01-release",
      "commit_count": 31,
      "repo_name": "repo.git",
      "release_date": "2016-03-16"
    }
  },
  "links": {
    "self": "/projects/4ef62672-22aa-4eb7-92c3-dee8495fac4b"
  }
}
```

This endpoint retrieves a specific project via its UUID.

### HTTP Request

`GET /projects/<UUID>`

<br />
**URL parameters**

Parameter | Description
--------- | -----------
UUID      | A UUID according to [RFC 4122](https://tools.ietf.org/html/rfc4122.html) which identifies the project.


## List

```python
import requests

response = requests.get("/projects")
```

```shell
curl -i "/projects"
```

> Below is an example of the data the above command may give:

```json
{
  "data": [
    {
      "id": "4ef62672-22aa-4eb7-92c3-dee8495fac4b",
      "attributes": {
        "title": "Blinky",
        "branch_count": 3,
        "repo_owner": "ARM mbed",
        "license": "Apache 2.0",
        "fork_count": 1024,
        "provider": "GitHub",
        "url": "https://github.com/ARMmbed/example-mbedos-blinky",
        "imports": 5043,
        "protocol": "git",
        "summary": "Simple example program to blink an LED on an mbed board with mbed OS",
        "description": null,
        "follower_count": 3064,
        "version": "mbedos-16.01-release",
        "commit_count": 31,
        "repo_name": "repo.git",
        "release_date": "2016-03-16"
      }
    },
    ...
  ],
  "links": {
    "self": "/projects?offset=0&limit=10",
    "next": "/projects?offset=10&limit=10"
  }
}
```

This endpoint retrieves a list of projects.

The list endpoint is paginated with a default limit of 10 results per page and
a maximum limit of 100. Pagination is done using a limit and offset parameter.
The results retrieved from this endpoint can also be sorted and filtered on the
resource's attributes. 

### HTTP Request

`GET /projects`

<br />
**Query parameters**

Parameter | Default | Description
--------- | ------- | -----------
`limit`   | 10      | The number of resources to be retrieved, maximum value of 100. 
`offset`  | 0       | The offset at which to start the list of resources.
`sort`    | N\A     | Sort the results by a given field's values e.g. `sort=value`. Value can be prefixed with a `-` character for descending order.


### Filtering

You can filter the results that are retrieved from the API by applying logical
operators on the fields of the resource you are retrieving. The filter is simply
a GET parameter. The following syntax is required for the filter argument:

`[field],op=value`

Mutliple filters may be used in a single request.

<br />
**Filter parameters**

Parameter | Description
--------- | -----------
`field`   | The field parameter must correspond to a field that belongs to the resource you are filtering.
`op`      | This is the logical operator to apply. See the filter operators table below.
`value`   | This is the value the operator uses to filter the resources by.

<br />
**Filter operators**

Operator | Description              | Logical representation
-------- | ------------------------ | ----------------------
`eq`     | equal to                 | `==`
`ne`     | not equal                | `!=`
`gt`     | greater than             | `>`
`lt`     | less than                | `<`
`ge`     | greater than or equal to | `>=`
`le`     | less than or equal to    | `<=`

<br />
**Example requests using filters**

Get a list of projects with the Apache 2.0 license  
`GET /projects?[license],eq=Apache 2.0`

Get a list of projects where number of imports are greater than 500  
`GET /projects?[imports],gt=500`

You can also use mutliple filters in a single request, e.g. get a list of
projects where the vcs is git, the supported mbed OS version is 5, and the
project's license is MIT  
`GET /projects?[protocol],eq=git&[mbed_os_version],eq=5&[license],eq=MIT`


## Create

```python
import requests

data = {
    "data": {
        "type": "project",
        "attributes": {
            "title": "Temperature Sensor",
            "url": "https://github.com/ARMmbed/example-mbedos-tmp",
        }
    }
}
headers = {
    "Accept": "application/vnd.api+json",
    "Content-Type": "application/vnd.api+json"
}

response = requests.post("/projects", headers=headers, data=data)
```

```shell
curl -X POST /projects 
  -H "Accept: application/vnd.api+json"
  -H "Content-Type: application/vnd.api+json"
  -d '{"data":{"type":"project","attributes""{"title":"Temperature Sensor", "url":"https://github.com/ARMmbed/example-mbedos-tmp"}}}'
```

Use this endpoint to create a new project resource.

### HTTP Request

`POST /projects`

<br />
**Request data**  
JSON data must be supplied with a POST request. The data must conform to the
[JSON API spec](http://jsonapi.org) by taking the following structure:

<code>
{
  "data": {
      "type": "project",
      "attributes": {
          "url": \<project URL\>,
          "title": \<project title\>,
          ...
      }
  }
}
</code>

`attributes` can contain any of the valid project attributes, but `url` and `title`
are required.

<br />
**Response**  
The indexer will respond to a successful creation with a `201 CREATED` status
code, along with the newly created resource serialized as JSON.


## Modify

Use this endpoint to modify a project resource

### HTTP Request

`PATCH /projects/<UUID>`

<br />
**URL parameters**

Parameter | Description
--------- | -----------
UUID      | A UUID according to RFC 4122 which identifies the project.

<br />
**Request data**  
JSON data must be supplied with a PATCH request. The data must conform to the
[JSON API spec](http://jsonapi.org) by taking the following structure:

<code>
{
  "data": {
      "type": "project",
      "attributes": {
          ...
      }
  }
}
</code>

`attributes` can contain any of the valid project attributes. Attributes supplied
here will replace the project's current attributes.

<br />
**Response**  
The indexer will respond to a successful modification with a `200` status code,
along with the modified resource serialized as JSON.
