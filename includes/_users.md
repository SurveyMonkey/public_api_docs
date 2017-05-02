##Users and Teams

Use these endpoints to get user's account information, any [teams](http://help.surveymonkey.com/articles/en_US/kb/Groups) a user belongs to, the account information for the team's owner, and other members including their roles and whether or not they have accepted an invite into the team (are `active`). 

<aside class="notice">While our API uses the term group, SurveyMonkey's UI uses teams. These two terms refer to the same concept. Learn more about [teams in our Help Center](http://help.surveymonkey.com/articles/en_US/kb/Groups).</aside>

###/users/me

>Definition

```
GET https://api.surveymonkey.net/v3/users/me
```

>Example Request

```shell
curl -i -X GET -H "Authorization:bearer YOUR_ACCESS_TOKEN" -H "Content-Type": "application/json" https://api.surveymonkey.net/v3/users/me
```

```python
import requests

s = requests.Session()
s.headers.update({
  "Authorization": "Bearer %s" % YOUR_ACCESS_TOKEN,
  "Content-Type": "application/json"
})

url = "https://api.surveymonkey.net/v3/users/me" 
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
  "href": "https://api.surveymonkey.net/v3/users/me",
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
account_type | [SurveyMonkey plan](https://www.surveymonkey.com/pricing/?ut_source=dev_portal&amp;ut_source2=docs) the user has:    `basic`, `pro`, `unlimited`, `select_monthly`, `gold`, `platinum`, `select_yearly`, `temp_pro`, `pro_comp`, `zoom_pro`, `zoom_premium`, `enterprise_gold`, `enterprise_platinum` | String-ENUM
date_created | Date user's account was created | Date String
date_last_login | Date user last logged in | Date String in format YYYY-MM-DDTHH:MM:SS0000+HH:MM
scopes| Contains two arrays: `scopes`, listing the [scopes](#scopes) available to the user and `granted`, listing the [scopes](#scopes) the user has approved during Oauth | Object