###/groups

>Definition

```
GET https://api.surveymonkey.com/v3/groups
```

>Example Request

```shell
curl -i -X GET -H "Authorization:bearer YOUR_ACCESS_TOKEN" https://api.surveymonkey.com/v3/groups
```

```python
import requests

s = requests.Session()
s.headers.update({
  "Authorization": "Bearer %s" % YOUR_ACCESS_TOKEN,
  "Content-Type": "application/json"
})

url = "https://api.surveymonkey.com/v3/groups
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
    "name": "Test Team",
    "href": "http://api.surveymonkey.com/v3/groups/1234"
  }],
  "links": {
    "self": "https://api.surveymonkey.com/v3/groups?page=1&per_page=1"
  }
}
```

####Available Methods

 * `HEAD`: Checks if resource is available
 * `OPTIONS`: Returns available methods and options
 * `GET`: Returns a team if the user account belongs to a [team](http://help.surveymonkey.com/articles/en_US/kb/Groups) (users can only belong to one team). Public App users need access to the **View Teams** [scope](#scopes)

####Optional Query Strings for GET

Name | Description | Data Type
------ | ------- | -------
page | Which page of resources to return. Defaults to 1 | Integer
per_page | Number of resources to return per page | Integer

####Groups List Resource

Name | Description | Data Type
------ | ------- | -------
data[\_].id | Group id | String
data[\_].name | Group name | String
data[\_].href | Resource API URL | String

###/groups/{id}

>Definition

```
GET https://api.surveymonkey.com/v3/groups/{group_id}
```

>Example Request

```shell
curl -i -X GET -H "Authorization:bearer YOUR_ACCESS_TOKEN" https://api.surveymonkey.com/v3/groups/1234
```

```python
import requests

s = requests.Session()
s.headers.update({
  "Authorization": "Bearer %s" % YOUR_ACCESS_TOKEN,
  "Content-Type": "application/json"
})

url = "https://api.surveymonkey.com/v3/groups/%s" % (group_id)
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
 * `GET`: Returns a teams's details including the teams's owner and email address. Public App users need access to the **View Teams** [scope](#scopes)

####Group Resource if Account Owner or Admin

Name | Description | Data Type
------ | ------- | -------
id | Group id | String
name | Group name | String
member_count | Number of members in the group | Integer
max_invites | Maximum number of members that can be in the group | Integer
date_created | Date and time when group was created | Date string

####Group Resource if Member

Name | Description | Data Type
------ | ------- | -------
id | Group id | String
name | Name of the group | String
owner_email | Group owner's email address | String

###/groups/{id}/members

>Definition

```
GET https://api.surveymonkey.com/v3/groups/{group_id}/members
```

>Example Request

```shell
curl -i -X GET -H "Authorization:bearer YOUR_ACCESS_TOKEN" -H "Content-Type": "application/json" https://api.surveymonkey.com/v3/groups/1234/members
```

```python
import requests

s = requests.Session()
s.headers.update({
  "Authorization": "Bearer %s" % YOUR_ACCESS_TOKEN,
  "Content-Type": "application/json"
})

url = "https://api.surveymonkey.com/v3/groups/%s/members" % (group_id)
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
    "self": "https://api.surveymonkey.com/v3/groups/12345/members?page=1&per_page=1"
  }
}
```

####Available Methods

 * `HEAD`: Checks if resource is available
 * `OPTIONS`: Returns available methods and options
 * `GET`: Returns a list of users who have been added as members of the specified group. Public App users need access to the **View Teams** [scope](#scopes)

####Optional Query Strings for GET

Name | Description | Data Type
------ | ------- | -------
page | Which page of resources to return. Defaults to 1 | Integer
per_page | Number of resources to return per page | Integer

####Group Members List Resource

Name | Description | Data Type
------ | ------- | -------
data[\_].id | Member id | String
data[\_].username | Member username | String
data[\_].href | Resource API URL | String


###/groups/{id}/members/{id}

>Definition

```
GET https://api.surveymonkey.com/v3/groups/{group_id}/members/{member_id}
```

>Example Request

```shell
curl -i -X GET -H "Authorization:bearer YOUR_ACCESS_TOKEN" -H "Content-Type": "application/json" https://api.surveymonkey.com/v3/groups/1234/members/1234
```

```python
import requests

s = requests.Session()
s.headers.update({
  "Authorization": "Bearer %s" % YOUR_ACCESS_TOKEN,
  "Content-Type": "application/json"
})

url = "https://api.surveymonkey.com/v3/groups/%s/members/%s" % (group_id, member_id)
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
 * `GET`: Returns a group member's details including their `role` and `status`. Public App users need access to the **View Teams** [scope](#scopes)

####Group Member Resource

Name | Description | Data Type
------ | ------- | -------
id | Member id | String
username | Member username | String
email| User's email address | String
type | Which type of [role](http://help.surveymonkey.com/articles/en_US/kb/Managing-Users#roles) the member has: `regular`,  `account_owner`, or `admin` | String-ENUM
status | A members [status](help.surveymonkey.com/articles/en_US/kb/Managing-Users#statuses) (if they have accepted an invitation into the group): `active`, `pending` | String-ENUM
user_id | User ID of the group member | String
date_created | Date and time when member was created | DateString

###/groups/{id}/activities

>Definition

```
GET https://api.surveymonkey.com/v3/groups/{group_id}/activities
```

>Example Request

```shell
curl -i -X GET -H "Authorization:bearer YOUR_ACCESS_TOKEN" -H "Content-Type": "application/json" https://api.surveymonkey.com/v3/groups/1234/activities
```

```python
import requests

s = requests.Session()
s.headers.update({
  "Authorization": "Bearer %s" % YOUR_ACCESS_TOKEN,
  "Content-Type": "application/json"
})

url = "https://api.surveymonkey.com/v3/groups/%s/activities" % (group_id)
s.get(url)
```

>Example Response

```json
{
   "sl_translate":"activity_msg,member_type",
   "total":1,
   "offset":0,
   "limit":20,
   "results":[      

{
         "date_created":"2020-01-02 03:04:05",
         "ip_address":"1.2.3.4",
         "city":null,
         "user_name":"test_user",
         "division_name":null,
         "group_id":1234,
         "activity_type":"collector_info_created",
         "user_id":1234,
         "activity_msg":"<span>Created web link collector <span class=\"notranslate\"><b>Collector name<\/b><\/span><\/span>",
         "email":"test@test.com",
         "member_type":"<span>(Primary Admin)<\/span>",
         "country":null

      }
]
}
```

####Available Methods

 * `GET`: Returns a list of activity related data for the specified group. Public App users must be admin.

####Optional Query Strings for GET

Name | Description | Data Type
------ | ------- | -------
limit | Max number of rows returned. Defaults to 50 | Integer
offset | Offset for the results, i.e., the number of rows skipped | Integer
start_date | The start date for the activity related data query | Date
end_date | The end date for the activity related data query | Date

####Activity List Resource

Name | Description | Data Type
------ | ------- | -------
results[\_].date_created | Activity creation date | Date
results[\_].ip_address | IP logged for activity | String
results[\_].user_name | Username logged for activity | String
results[\_].group_id | Group ID logged for activity | Integer
results[\_].activity_type | Type of activity | String-ENUM
results[\_].user_id | User ID logged for activity | Integer
results[\_].activity_msg | Message for activity | Stirng-HTML
results[\_].email | Email logged for activity | String
results[\_].member_type | Member type for activity | String-HTML


###/groups/{id}/activities/{activity_type}?interval={internal}

>Definition

```
GET https://api.surveymonkey.com/v3/groups/{group_id}/activities/{activity_type}
```

>Example Request

```shell
curl -i -X GET -H "Authorization:bearer YOUR_ACCESS_TOKEN" -H "Content-Type": "application/json" https://api.surveymonkey.com/v3/groups/1234/activities/1234?interval=daily
```

```python
import requests

s = requests.Session()
s.headers.update({
  "Authorization": "Bearer %s" % YOUR_ACCESS_TOKEN,
  "Content-Type": "application/json"
})

url = "https://api.surveymonkey.com/v3/groups/%s/activities/%s?interval=%s" % (group_id, activity_type)
s.get(url)
```

>Example Response

```json
{"series":[86,193],"times":["2020","2019"],"interval":"yearly"}
```

####Available Methods

 * `GET`: Returns a count of a specific activity by interval for the specified group given an activity type enum value. Public App users must be admin

####Required Query Strings for GET
Name | Description | Data Type
------ | ------- | -------
interval | Interval of the series data to return | String-ENUM (One of "daily", "weekly", "monthly", "yearly")

####Optional Query Strings for GET

Name | Description | Data Type
------ | ------- | -------
start_date | The start date for the activity related data query | Date
end_date | The end date for the activity related data query | Date

####Activity Type Enum Values
 * authentication_succeeded
 * authentication_failed
 * authentication_signout
 * group_info_updated_group_name
 * invite_created
 * invite_resent
 * member_deleted
 * member_joined
 * survey_info_create
 * survey_info_delete
 * survey_info_copy
 * survey_info_update
 * survey_info_transfer
 * collector_info_created
 * collector_info_deleted
 * collector_info_updated
 * member_updated_group_member_type
 * permission_created
 * permission_updated
 * shared_view_created
 * shared_view_updated
 * export_export_create
 * export_downloaded
 * respondent_updated
 * respondent_deleted
 * grant_info_created
 * grant_info_deleted

####Activity List Resource

Name | Description | Data Type
------ | ------- | -------
series | Series data of the count of the specified activity type per interval period | Array of Integers,
times | Labels of times for series data set | Array of String,
interval | The interval for the returned series | String

