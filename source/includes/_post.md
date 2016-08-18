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

<br />
**HTTP Request**

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

<br />
**Errors**

The following HTTP errors can arise if there are errors in the request. Please see
the [content negotiation](http://jsonapi.org/format/#content-negotiation-servers)
and [create responses](http://jsonapi.org/format/#crud-creating-responses) sections
of the JSON API spec for more detail as to why these errors can occur.

Status                       | Description
---------------------------- | -----------
`403 FORBIDDEN`              | Request's JSON data does not conform to JSON spec.
`406 NOT ACCEPTABLE`         | Request's Accept header does not conform to JSON spec.
`415 UNSUPPORTED MEDIA TYPE` | Request's media type does not conform to JSON spec.
