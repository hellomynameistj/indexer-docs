## Modify

```python
import requests

data = {
    "data": {
        "type": "project",
        "attributes": {
            "title": "A new title for my project",
        }
    }
}
headers = {
    "Accept": "application/vnd.api+json",
    "Content-Type": "application/vnd.api+json"
}

response = requests.patch("/projects", headers=headers, data=data)
```

```shell
curl -X PATCH /projects 
  -H "Accept: application/vnd.api+json"
  -H "Content-Type: application/vnd.api+json"
  -d '{"data":{"type":"project","attributes""{"title":"A new title for my project"}}}'
```

Use this endpoint to modify a project resource

<br />
**HTTP Request**

`PATCH /projects/<UUID>`

<br />
URL parameters:

Parameter | Description
--------- | -----------
UUID      | A UUID according to [RFC 4122](https://tools.ietf.org/html/rfc4122.html) which identifies the project.

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

`attributes` can contain any of the valid editable project attributes. Attributes
supplied here will replace the project's current attributes.

<br />
**Response**  
The indexer will respond to a successful modification with a `200` status code,
along with the modified resource serialized as JSON.

<br />
**Errors**

The following HTTP errors can arise if there are errors in the request. Please see
the [content negotiation](http://jsonapi.org/format/#content-negotiation-servers)
and [update responses](http://jsonapi.org/format/#crud-updating-responsess) sections
of the JSON API spec for more detail as to why these errors can occur.

Status                       | Description
---------------------------- | -----------
`404 NOT FOUND`              | UUID does not match existing resource.
`403 FORBIDDEN`              | Request's JSON data does not conform to JSON spec.
`406 NOT ACCEPTABLE`         | Request's Accept header does not conform to JSON spec.
`409 CONFLICT`               | The required `id` or `type` fields in the request's JSON document do not match the resource.
`415 UNSUPPORTED MEDIA TYPE` | Request's media type does not conform to JSON spec.
