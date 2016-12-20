##Users and Groups

Use these endpoints to get user's account information, any [groups](http://help.surveymonkey.com/articles/en_US/kb/Groups) a user belongs to, and the account information for the group's owner and other members including their roles and whether or not they have accepted an invite into the group (are `active`). 

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
 * `GET`: Returns the current user's account details including their plan. Requires **View Users** [scope](#scopes)

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
  "date_last_login": "2015-10-06T12:56:55+00:00"
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
date_created | Date user's account was created | DateString
date_last_login | Date user last logged in | DateString