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
  "id": "123",
  "username": "test-user",
  "first_name": "John",
  "last_name": "Doe",
  "language": "en",
  "email": "test@surveymonkey.com",
  "account_type": "enterprise_platinum",
  "date_created": "2015-10-06T12:56:55+00:00",
  "date_last_login": "2015-10-06T12:560000:55+00:00"
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