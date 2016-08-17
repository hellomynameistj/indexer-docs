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
