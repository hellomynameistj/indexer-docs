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
  "links": {
    "self": "/projects/4ef62672-22aa-4eb7-92c3-dee8495fac4b"
  }
}
```

This endpoint retrieves a specific project via its UUID.

<br />
**HTTP Request**

`GET /projects/<UUID>`

<br />
URL parameters:

Parameter | Description
--------- | -----------
UUID      | A UUID according to [RFC 4122](https://tools.ietf.org/html/rfc4122.html) which identifies the project.
