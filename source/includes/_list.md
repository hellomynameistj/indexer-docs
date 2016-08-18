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
        "protocol": "Git",
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

<br />
**HTTP Request**

`GET /projects`

<br />
Query parameters:

Parameter | Default | Description
--------- | ------- | -----------
limit     | 10      | The number of resources to be retrieved, maximum value of 100. 
offset    | 0       | The offset at which to start the list of resources.
sort      | N\A     | Sort the results by a given field's values e.g. `sort=<field>`. `field` can be prefixed with a `-` character for descending order.

<br />
**Pagination**

The JSON response includes a top-level key `links` which includes the URL for
current requested page (`self`) along with the URLs for the next and previous pages
(`next` and `prev` respectively). These links can be used to page through the
requested set by making GET requests on these URLs. The final page will not have
a `next` key in the `links` section, and the first page will not have a `prev` key.
See the code panel on the right for an example.

<br />
**Filtering**

You can filter the results that are retrieved from the API by applying logical
operators on the fields of the resource you are retrieving. The filter is simply
a GET parameter. The following syntax is required for the filter argument:

`[field],op=value`

Mutliple filters may be used in a single request.

<br />
Filter parameters:

Parameter | Description
--------- | -----------
field     | The field parameter must correspond to a field that belongs to the resource you are filtering.
op        | This is the logical operator to apply. See the filter operators table below.
value     | This is the value the operator uses to filter the resources by.

<br />
Filter operators:

Operator | Description              | Logical representation
-------- | ------------------------ | ----------------------
eq       | equal to                 | `==`
ne       | not equal                | `!=`
gt       | greater than             | `>`
lt       | less than                | `<`
ge       | greater than or equal to | `>=`
le       | less than or equal to    | `<=`

<br />
Example requests using filters:

Get a list of projects with the Apache 2.0 license  
`GET /projects?[license],eq=Apache 2.0`

Get a list of projects where number of imports are greater than 500  
`GET /projects?[imports],gt=500`

You can also use mutliple filters in a single request, e.g. get a list of
projects where the vcs is git, the supported mbed OS version is 5, and the
project's license is MIT  
`GET /projects?[protocol],eq=Git&[mbed_os_version],eq=5&[license],eq=MIT`

<br />
**Response**  
The indexer will respond to a successful fetch with a `200` status code, along
with a list of the fetched resources serialized as JSON.

<br />
**Errors**

The following HTTP errors can arise if there are errors in the request. Please see
the [content negotiation](http://jsonapi.org/format/#content-negotiation-servers)
and [fetch responses](http://jsonapi.org/format/#fetching-resources-responses) sections
of the JSON API spec for more detail as to why these errors can occur.

Status                       | Description
---------------------------- | -----------
`400 BAD REQUEST`            | Request's GET parameters are invalid/badly formatted.
`406 NOT ACCEPTABLE`         | Request's Accept header does not conform to JSON spec.
`415 UNSUPPORTED MEDIA TYPE` | Request's media type does not conform to JSON spec.
