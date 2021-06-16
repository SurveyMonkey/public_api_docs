##Errors

Get a list of errors or lookup an error by its id. See also [error codes](#error-codes).

###/errors

>Definition

```
GET https://api.surveymonkey.com/v3/errors
```

>Example Request

```shell
curl -i -X GET -H "Authorization:bearer YOUR_ACCESS_TOKEN" https://api.surveymonkey.com/v3/errors
```

```python
import requests

s = requests.session()
s.headers.update({
  "Authorization": "Bearer %s" % YOUR_ACCESS_TOKEN,
  "Content-Type": "application/json"
})

url = "https://api.surveymonkey.com/v3/errors"
s.get(url)
```

>Example Response

```json
{
  "page": 1,
  "per_page": 1,
  "total": 1,
  "data": [{
    "id": "1234",
    "href": "https://api.surveymonkey.com/v3/errors/1234",
    "name": "Known Error"
  }],
  "links": {
    "self": "https://api.surveymonkey.com/v3/errors?page=1&per_page=1"
  }
}
```
####Available Methods

 * `HEAD`: Checks if resource is available
 * `OPTIONS`: Returns available methods and options
 * `GET`: Returns a list of known errors

####Optional Query Strings for GET

Name | Description | Data Type
------ | ------- | -------
page | Page of resources to return. Defaults to 1 | Integer
per_page | Number of resources to return per page | Integer

####Errors list Resource

Name | Description | Data Type
------ | ------- | -------
data[\_].id | Error id | String
data[\_].href  | Resource API URL | String
data[\_].name | Error name | String


###/errors/{id}

>Definition

```
GET https://api.surveymonkey.com/v3/errors/{error_id}
```

>Example Request

```shell
curl -i -X GET -H "Authorization:bearer YOUR_ACCESS_TOKEN" https://api.surveymonkey.com/v3/errors/1234
```

```python
import requests

s = requests.session()
s.headers.update({
  "Authorization": "Bearer %s" % YOUR_ACCESS_TOKEN,
  "Content-Type": "application/json"
})

url = "https://api.surveymonkey.com/v3/errors/%s" % (error_id)
s.get(url)
```

>Example Response

```json
{
  "id": "1234",
  "message": "This is an error.",
  "href": "https://api.surveymonkey.com/v3/errors/1234",
  "name": "Known Error",
  "docs": "https://developer.surveymonkey.com/api/v3/#error-codes"
}
```

####Available Methods

 * `HEAD`: Checks if resource is available
 * `OPTIONS`: Returns available methods and options
 * `GET`: Returns the details of a known error

####Error Resource

Name | Description | Data Type
------ | ------- | -------
id | Error id | String
message | Error explanation | String
href | Resource API URL | String
docs | Error documentation page | String
name | Error name | String



