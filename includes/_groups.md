###/groups

>Definition

```
GET https://api.surveymonkey.net/v3/groups
```

>Example Request

```shell
curl -i -X GET -H "Authorization:bearer YOUR_ACCESS_TOKEN" https://api.surveymonkey.net/v3/groups?api_key=YOUR_API_KEY
```

```python
import requests

s = requests.Session()

url = "https://api.surveymonkey.net/v3/groups?api_key=%s" % YOUR_API_KEY
s.get(url)
```

>Example Response

```json
{
  "per_page": 1,
  "page": 1,
  "total": 1,
  "data": [{
    "id": "1234",
    "name": "Test Group",
    "href": "http://api.surveymonkey.com/v3/groups/1234"
  }],
  "links": {
    "self": "https://api.surveymonkey.net/v3/groups?page=1&per_page=1"
  }
}
```

####Available Methods

 * `HEAD`: Checks if resource is available
 * `OPTIONS`: Returns available methods and options
 * `GET`: Returns a group if the user account belongs to a [group](http://help.surveymonkey.com/articles/en_US/kb/Groups) (users can only belong to one group)

####Optional Query Strings for GET

Name | Description | Type
------ | ------- | -------
page | Which page of resources to return. Defaults to 1 | Integer
per_page | Number of resources to return per page | Integer

####Groups List Resource

Name | Description | Type
------ | ------- | -------
data[_].id | Group id | String
data[_].name | Group name | String
data[_].href | Resource API URL | String

###/groups/{id}

>Definition

```
GET https://api.surveymonkey.net/v3/groups/{group_id}
```

>Example Request

```shell
curl -i -X GET -H "Authorization:bearer YOUR_ACCESS_TOKEN" https://api.surveymonkey.net/v3/groups/1234?api_key=YOUR_API_KEY
```

```python
import requests

s = requests.Session()

url = "https://api.surveymonkey.net/v3/groups/%s?api_key=%s" % (group_id, YOUR_API_KEY)
s.get(url)
```

>Example Response

```json
{
  "id": "1234",
  "name": "Test Group",
  "member_count": 1,
  "max_invites": 100,
  "date_created": "2015-10-06T12:56:55+00:00"
}
```

####Available Methods

 * `HEAD`: Checks if resource is available
 * `OPTIONS`: Returns available methods and options
 * `GET`: Returns a group's details including the group's owner and email address

####Group Resource if Account Owner or Admin 

Name | Description | Type
------ | ------- | -------
id | Group id | String
name | Group name | String
member_count | Number of members in the group | String
max_invites | Maximum number of members that can be in the group | String
date_created | Date and time when group was created | String

####Group Resource if Member

Name | Description | Type
------ | ------- | -------
id | Group id | String
name | Name of the group | String
owner_email | Group owner's email address | String

###/groups/{id}/members

>Definition

```
GET https://api.surveymonkey.net/v3/groups/{group_id}/members
```

>Example Request

```shell
curl -i -X GET -H "Authorization:bearer YOUR_ACCESS_TOKEN" https://api.surveymonkey.net/v3/groups/1234/members?api_key=YOUR_API_KEY
```

```python
import requests

s = requests.Session()

url = "https://api.surveymonkey.net/v3/groups/%s/members?api_key=%s" % (group_id, YOUR_API_KEY)
s.get(url)
```

>Example Response

```json
{
  "per_page": 1,
  "page": 1,
  "total": 1,
  "data": [{
    "id": "1234",
    "username": "test_user",
    "href": "http://api.surveymonkey.com/v3/members/1234"
  }],
  "links": {
    "self": "https://api.surveymonkey.net/v3/groups/12345/members?page=1&per_page=1"
  }
}
```

####Available Methods

 * `HEAD`: Checks if resource is available
 * `OPTIONS`: Returns available methods and options
 * `GET`: Returns a list of users who have been added as members of the specified group  

####Optional Query Strings for GET

Name | Description | Type
------ | ------- | -------
page | Which page of resources to return. Defaults to 1 | Integer
per_page | Number of resources to return per page | Integer

####Group Members List Resource

Name | Description | Type
------ | ------- | -------
data[_].id | Member id | String
data[_].username | Member username | String
data[_].href | Resource API URL | String


###/groups/{id}/members/{id}

>Definition

```
GET https://api.surveymonkey.net/v3/groups/{group_id}/members/{member_id}
```

>Example Request

```shell
curl -i -X GET -H "Authorization:bearer YOUR_ACCESS_TOKEN" https://api.surveymonkey.net/v3/groups/1234/members/1234?api_key=YOUR_API_KEY
```

```python
import requests

s = requests.Session()

url = "https://api.surveymonkey.net/v3/groups/%s/members/%s?api_key=%s" % (group_id, member_id, YOUR_API_KEY)
s.get(url)
```

>Example Response

```json
{
  "id": "1234",
  "username": "test_user",
  "email": "test@surveymonkey.com",
  "type": "regular",
  "status": "active",
  "user_id": "1234",
  "date_created": "2015-10-06T12:56:55+00:00"
}
```

####Available Methods

 * `HEAD`: Checks if resource is available
 * `OPTIONS`: Returns available methods and options
 * `GET`: Returns a group member's details including their `role` and `status`

####Group Member Resource

Name | Description | Type
------ | ------- | -------
id | Member id | String
username | Member username | String
email| User's email address | String
type | Which type of [role](http://help.surveymonkey.com/articles/en_US/kb/Managing-Users#roles) the member has: 'regular', 'account_owner', or 'admin' | String
status | A members [status](help.surveymonkey.com/articles/en_US/kb/Managing-Users#statuses) (if they have accepted an invitation into the group):'active', 'pending' | String
user_id | User ID of the group member | String
date_created | Date and time when member was created | String
