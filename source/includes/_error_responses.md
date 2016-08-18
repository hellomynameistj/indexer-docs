## Error Responses

> Below is an example of the error response JSON data if the `limit` GET parameter
is set to a negative value:

```json
{
  "errors": [
    {
      "status": 400,
      "title": "Bad request",
      "detail": "limit parameter must be a positive integer"
    }
  ]
}
```

HTTP error responses are returned with a JSON document describing the errors.
This provides more context about the error. See the example in the panel on the right.
