##Users and Teams

Use these endpoints to get user's account information, any [teams](http://help.surveymonkey.com/articles/en_US/kb/Groups) a user belongs to, the account information for the team's owner, and other members including their roles and whether or not they have accepted an invite into the team (are `active`).

<aside class="notice">While our API uses the term group, SurveyMonkey's UI uses teams. These two terms refer to the same concept. Learn more about [teams in our Help Center](http://help.surveymonkey.com/articles/en_US/kb/Groups).</aside>

###/users/me

>Definition

```
GET https://api.surveymonkey.com/v3/users/me
```

>Example Request

```shell
curl -i -X GET -H "Authorization:bearer YOUR_ACCESS_TOKEN" -H "Content-Type": "application/json" https://api.surveymonkey.com/v3/users/me
```

```python
import requests

s = requests.Session()
s.headers.update({
  "Authorization": "Bearer %s" % YOUR_ACCESS_TOKEN,
  "Content-Type": "application/json"
})

url = "https://api.surveymonkey.com/v3/users/me"
s.get(url)
```

####Available Methods

 * `HEAD`: Checks if resource is available
 * `OPTIONS`: Returns available methods and options
 * `GET`: Returns the current user's account details including their plan. Public App users need access to the **View Users** [scope](#scopes)

####User Resource

>Example Response

```json
{
  "username": "testuser",
  "scopes": {
    "available": [
      "users_read",
      "surveys_read",
      "collectors_read",
      "collectors_write",
      "contacts_read",
      "contacts_write",
      "surveys_write",
      "responses_read",
      "responses_read_detail",
      "responses_write",
      "groups_read",
      "webhooks_read",
      "webhooks_write",
      "library_read"
    ],
    "granted": [
      "collectors_read",
      "contacts_write",
      "contacts_read",
      "surveys_read",
      "collectors_write",
      "users_read"
    ]
  },
  "first_name": "Test",
  "last_name": "User",
  "account_type": "enterprise_platinum",
  "language": "en",
  "email": "user@surveymonkey.com",
  "email_verified": true,
  "href": "https://api.surveymonkey.com/v3/users/me",
  "date_last_login": "2017-04-28T03:49:24.333000+00:00",
  "date_created": "2015-12-03T01:23:00+00:00",
  "id": "1234"
}
```

Name | Description | Data Type
------ | ------- | -------
id | User id | String
username | Username | String
first_name | User's first name | String
last_name | User's last name | String
language | ISO 639-1 code for the language set for the user's account | String-ENUM
email | Email address for user's account | String
email_verified | Email address for user's account has been verified | Boolean
account_type | [SurveyMonkey plan](https://www.surveymonkey.com/pricing/?ut_source=dev_portal&amp;ut_source2=docs) the user has | String-ENUM
date_created | Date user's account was created | Date String
date_last_login | Date user last logged in | Date String in format YYYY-MM-DDTHH:MM:SS0000+HH:MM
scopes | Contains two arrays: `available`, listing the [scopes](#scopes) available to the user and `granted`, listing the [scopes](#scopes) the user has approved during Oauth | Object

###/users/{id}/workgroups

>Definition

```
GET https://api.surveymonkey.com/v3/users/{user_id}/workgroups
```

>Example Request

```shell
curl -i -X GET -H "Authorization:bearer YOUR_ACCESS_TOKEN" -H "Content-Type": "application/json" https://api.surveymonkey.com/v3/users/{user_id}/workgroups

```python
import requests

s = requests.Session()
s.headers.update({
  "Authorization": "Bearer %s" % YOUR_ACCESS_TOKEN,
  "Content-Type": "application/json"
})

url = "https://api.surveymonkey.com/v3/users/%s/workgroups" % user_id
s.get(url)
```

>Example Response

```json
TODO
```

####Available Methods

 * `HEAD`: Checks if resource is available
 * `OPTIONS`: Returns available methods and options
 * `GET`: Returns the workgroups that a specific user is in. Public App users need access to the **View Workgroups** [scope](#scopes)

####Optional Query Strings for GET

Name | Description | Data Type
------ | ------- | -------
page | Which page of resources to return. Defaults to 1 | Integer
per_page | Number of resources to return per page | Integer

####Workgroups List Resource

Name | Description | Data Type
------ | ------- | -------
data[\_].id | ID of the workgroup | String
data[\_].name | Name of the workgroup | String
data[\_].description | Description of the workgroup | String
data[\_].is_visible | Whether the workgroup is publicly visible or only visible to its members and administrators | Boolean
data[\_].created_at | Datetime when the workgroup was created | DateTime
data[\_].updated_at | Datetime when the workgroup was last updated | DateTime
data[\_].members | The active members of the workgroup. | Array
data[\_].shares_count | Number of resources shared with the workgroup | Integer
data[\_].members_count | Number of members in the workgroup (includes non-active) | Integer
data[\_].default_role | The default role for the workgroup | Object
data[\_].membership | Membership information for the requested user | Object

###/users/{id}/shared

>Definition

```
GET https://api.surveymonkey.com/v3/users/{user_id}/shared
```

>Example Request

```shell
curl -i -X GET -H "Authorization:bearer YOUR_ACCESS_TOKEN" -H "Content-Type": "application/json" https://api.surveymonkey.com/v3/users/{user_id}/shared
```

```python
import requests

s = requests.Session()
s.headers.update({
  "Authorization": "Bearer %s" % YOUR_ACCESS_TOKEN,
  "Content-Type": "application/json"
})

url = "https://api.surveymonkey.com/v3/users/%s/shared" % user_id
s.get(url)
```

>Example Response

```json
TODO
```

####Available Methods

 * `HEAD`: Checks if resource is available
 * `OPTIONS`: Returns available methods and options
 * `GET`: Returns the resources shared with a user across all workgroups. Public App users need access to the **View Workgroup Shares** [scope](#scopes)

####Optional Query Strings for GET

Name | Description | Data Type
------ | ------- | -------
page | Which page of resources to return. Defaults to 1 | Integer
per_page | Number of resources to return per page | Integer
resource_type | The type of the shared resource, one of: `survey` | String-ENUM
resource_id | Comma separated IDs of shared resources (must be used with resource_type) | Comma Separated String-ENUM
include | Specify additional fields to return for each resource: `permissions`, `resource_details` | Comma Separated String-ENUM

####Workgroup Shares List Resource

Name | Description | Data Type
------ | ------- | -------
data[\_].share_id | ID of the share record | String
data[\_].workgroup_id | D of the workgroup that was shared with | String
data[\_].owner_user_id | The ID of the user who shared the resource | String
data[\_].resource_type | The type of the shared resource (e.g. `survey`) | String-ENUM
data[\_].resource_id | The ID of the shared resource (e.g. the ID of a survey) | String
data[\_].privileges | An array of scoped privileges granted to the user by this share record | Array
