## Modify

Use this endpoint to modify a project resource

### HTTP Request

`PATCH /projects/<UUID>`

<br />
**URL parameters**

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
