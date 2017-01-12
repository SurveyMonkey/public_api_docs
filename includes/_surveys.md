##Surveys, Pages, and Questions

The following endpoints let you create surveys, survey pages, and add questions to survey pages.

A POST to /surveys will create an empty survey to which you can add [pages](#surveys-id-pages) and [questions](#surveys-id-pages-id-questions) (See [formatting question types](#formatting-question-types)). This endpoint also accepts a survey or template ID as an arguement to create a pre-populated survey that can be used as is or modified by deleting, updating, or adding pages or questions.

A survey needs at least one page and question in order to record a survey [response](#surveys-id-responses).

<aside class="notice"><strong>NOTE for Public Apps</strong>: The View Surveys scope is available on the BASIC (Free) plan and the Create/Modify Surveys scope requires a <a href="https://www.surveymonkey.com/pricing/?ut_source=dev_portal&amp;ut_source2=docs">paid plan</a>.</aside>


###/surveys

>Definition

```
POST https://api.surveymonkey.net/v3/surveys
```


>Example Request

```shell
curl -i -X POST -H "Authorization:bearer YOUR_ACCESS_TOKEN" -H "Content-Type": "application/json" https://api.surveymonkey.net/v3/surveys -d '{"title":"My Survey"}'
```

```python
import requests

s = requests.Session()
s.headers.update({
  "Authorization": "Bearer %s" % YOUR_ACCESS_TOKEN,
  "Content-Type": "application/json"
})

payload = {
  "title": "My Survey"
}
url = "https://api.surveymonkey.net/v3/surveys"
s.post(url, json=payload)
```
>Example Response

```json
{
  "title": "My Survey",
  "nickname": "",
  "category":"",
  "language": "en",
  "question_count": 10,
  "page_count": 10,
  "date_created": "2015-10-06T12:56:55",
  "date_modified": "2015-10-06T12:56:55",
  "id": "1234",
  "href": "https://api.surveymonkey.com/v3/surveys/1234",
  "buttons_text": {
    "done_button": "Done",
    "prev_button": "Prev",
    "exit_button": "Exit",
    "next_button": "Next"
  },
  "custom_variables": {
    "name": "label"
  },
  "footer": true,
  "preview": "https://www.surveymonkey.com/r/Preview/",
  "edit_url": "https://www.surveymonkey.com/create/",
  "collect_url": "https://www.surveymonkey.com/collect/list",
  "analyze_url": "https://www.surveymonkey.com/analyze/",
  "summary_url": "https://www.surveymonkey.com/summary/"
}
```

####Available Methods

 * `HEAD`: Checks if resource is available
 * `OPTIONS`: Returns available methods and options
 * `GET`: Returns a list of surveys owned or shared with the authenticated user. Requires **View Surveys** [scope](#scopes)
 * `POST`: Creates a new empty survey or, if a [template](#survey_templates) id or an existing survey id is specified, a survey prepopulated with [pages](#surveys-id-pages) and [questions](#formatting-question-types). Requires **Create/Modify Surveys** [scope](#scopes)

####Optional Query Strings for GET

Name | Description | Data Type
------ | ------- | -------
page | Which page of resources to return. Defaults to 1 | Integer
per_page | Number of resources to return per page | Integer
sort_by | Field used to sort returned survey list: `title`, `date_modified`, or `num_responses` | String-ENUM
sort_order | Sort order: `ASC` or `DESC` | String-ENUM
include | Use to filter survey list: `shared_with', `shared_by`, or `owned` (useful for teams) or use to specify additional fields to return per survey: `response_count`, `date_created`, `date_modified`, `language`, `question_count`, `analyze_url`, `preview` |Comma Separated String-ENUM
title | Search survey list by survey title | String
start_modified_at | Surveys must be last modified after this date. | Date string in format YYYY-MM-DDTHH:MM:SS (no offset)
end_modified_at | Surveys must be last modified before this date. | Date string in format YYYY-MM-DDTHH:MM:SS (no offset)

####Survey List Resource

Name | Description | Data Type
------ | ------- | -------
data[\_].id | Survey id | String
data[\_].title | Survey title | String
data[\_].nickname | Survey nickname | String
data[\_].href | Resource API URL | String

####Request Body Arguments for POST (if copying from existing survey or template)

Name |Required| Description | Data Type
------ | ----- | ------- | -------
title | No (default="New Survey")|Survey title | String
from_template_id | No (required if from_survey_id not provided) | Survey template to copy from. See [/survey_templates](#survey_templates) | String
from_survey_id | No (required if from_template_id not provided) | Survey id to copy from | String

####Request Body Arguments for POST (if creating blank survey)

Name |Required| Description | Type
------ | ----- | ------- | -------
title | No (default="New Survey")|Survey title | String
nickname | No (default="")|Survey nickname | String
language | No (default="en") | Survey language | String
buttons_text | No | Survey Buttons text container | Object
buttons_text.next_button | No | Button text | String
buttons_text.prev_button | No | Button text | String
buttons_text.exit_button | No | Button text. If set to an empty string, button will be ommitted from survey | String
buttons_text.done_button | No | Button text | String
custom_variables | No | Dictionary of survey variables | Object
footer| No (default=true)| If false, SurveyMonkey's [footer](https://help.surveymonkey.com/articles/en_US/kb/How-do-I-turn-off-the-Powered-by-SurveyMonkey-branding) is not displayed | Boolean

####Request Body Arguments for Bulk POST

Name | Required | Description | Type
------ | ----- | ------- | -------
title | No (default="New Survey")|Survey title | String
nickname | No (default="")|Survey nickname | String
language | No (default="en") | Survey language | String
buttons_text | No | Survey Buttons text container | Objects
buttons_text.next_button | No | Button text | String
buttons_text.prev_button | No | Button text | String
buttons_text.exit_button | No | Button text. If set to an empty string, button will be ommitted from survey  | String
buttons_text.done_button | No | Button text | String
pages | Yes | Pages to be created | List of Page Objects
pages[\_].questions | Yes | Questions to be created | List of Question Objects
footer| No (default=true)| If false, SurveyMonkey's [footer](https://help.surveymonkey.com/articles/en_US/kb/How-do-I-turn-off-the-Powered-by-SurveyMonkey-branding) is not displayed | Boolean


###/surveys/{id}

>Definition

```
GET https://api.surveymonkey.net/v3/surveys/{survey_id}
```

>Example Request

```shell
curl -i -X GET -H "Authorization:bearer YOUR_ACCESS_TOKEN" -H "Content-Type": "application/json" https://api.surveymonkey.net/v3/surveys/1234
```

```python
import requests

s = requests.Session()
s.headers.update({
  "Authorization": "Bearer %s" % YOUR_ACCESS_TOKEN,
  "Content-Type": "application/json"
})

url = "https://api.surveymonkey.net/v3/surveys/%s" % (survey_id)
s.get(url)
```
>Example Response

```json
{
  "title": "My Survey",
  "nickname": "",
  "category": "",
  "language": "en",
  "question_count": 0,
  "page_count": 0,
  "date_created": "2015-10-06T12:56:55",
  "date_modified": "2015-10-06T12:56:55",
  "id": "1234",
  "href": "http://api.surveymonkey.com/v3/surveys/1234",
  "buttons_text": {
    "done_button": "Done",
    "prev_button": "Prev",
    "exit_button": "Exit",
    "next_button": "Next"
  },
  "custom_variables": {
    "name": "label"
  },
  "footer": true,
  "preview": "https://www.surveymonkey.com/r/Preview/",
  "edit_url": "https://www.surveymonkey.com/create/",
  "collect_url": "https://www.surveymonkey.com/collect/list",
  "analyze_url": "https://www.surveymonkey.com/analyze/",
  "summary_url": "https://www.surveymonkey.com/summary/",
  "response_count": 12
}
```
####Available Methods

 * `HEAD`: Checks if resource is available
 * `OPTIONS`: Returns available methods and options
 * `GET`: Returns a survey's details. To get an expanded version showing all pages and questions use [/surveys/{survey_id}/details](#surveys-id-details). Requires **View Surveys** [scope](#scopes)
 * `PATCH`: Modifies a survey's title, nickname or language. Requires **Create/Modify Surveys** [scope](#scopes)
 * `PUT`:  Replaces a survey. Request body arguments the same as POST [/surveys](#surveys). Requires **Create/Modify Surveys** [scope](#scopes)
 * `DELETE`: Deletes a survey. Requires **Create/Modify Surveys** [scope](#scopes)

####Request Body Arguments for PATCH (See POST [/surveys](#surveys) for PUT arguments)

Name | Required | Description | Data Type
------ | ----- | ------- | -------
title | No (`PUT` default="New Survey") |Survey title | String
nickname | No (`PUT` default="") |Survey nickname | String
language | No (`PUT` default="en") | Survey language | String
buttons_text | No | Survey Buttons text container | Object
buttons_text.next_button | No | Button text | String
buttons_text.prev_button | No | Button text | String
buttons_text.exit_button | No | Button text. If set to an empty string, button will be ommitted from survey | String
buttons_text.done_button | No | Button text | String
custom_variables | No | Dictionary of survey variables | Object
footer| No (default=true)| If false, SurveyMonkey's [footer](https://help.surveymonkey.com/articles/en_US/kb/How-do-I-turn-off-the-Powered-by-SurveyMonkey-branding) is not displayed | Boolean

####Survey Resource

Name | Description | Type
------ | ------- | -------
id | Survey id | String
title | Survey title | String
nickname | Survey nickname | String
custom_variables | Dictionary of survey variables | Object
category| Survey category chosen when creating the survey | String
language | ISO 639-1 code for survey language | String-ENUM
question_count | Number of questions in survey | Integer
page_count | Number of pages in survey | Integer
date_created | Date and time when survey was created | Date string in format YYYY-MM-DDTHH:MM:SS (no offset)
date_modified | Date and time when survey was last modified | Date string in format YYYY-MM-DDTHH:MM:SS (no offset)
buttons_text.next_button | Button text | String
buttons_text.prev_button | Button text | String
buttons_text.exit_button | Button text | String
buttons_text.done_button | Button text | String
preview | Survey preview URL | String
edit_url | Survey edit URL | String
collect_url | Survey collect URL | String
analyze_url | Survey analyze URL | String
summary_url | Survey summary URL | String
href | Resource API URL | String
response_count | Number of responses survey has received | Integer
footer | Whether or not SurveyMonkey's [footer](https://help.surveymonkey.com/articles/en_US/kb/How-do-I-turn-off-the-Powered-by-SurveyMonkey-branding) is not displayed | Boolean


###/surveys/{id}/details

>Definition

```
GET https://api.surveymonkey.net/v3/surveys/{survey_id}/details
```

>Example Request

```shell
curl -i -X GET -H "Authorization:bearer YOUR_ACCESS_TOKEN" -H "Content-Type": "application/json" https://api.surveymonkey.net/v3/surveys/1234/details
```

```python
import requests

s = requests.Session()
s.headers.update({
  "Authorization": "Bearer %s" % YOUR_ACCESS_TOKEN,
  "Content-Type": "application/json"
})

url = "https://api.surveymonkey.net/v3/surveys/%s/details" % (survey_id)
s.get(url)
```

>Example Response

```json
{
  "title": "My Survey",
  "nickname": "",
  "custom_variables": {
    "name": "label"
  },
  "language": "en",
  "question_count": 10,
  "page_count": 10,
  "date_created": "2015-10-06T12:56:55+00:00",
  "date_modified": "2015-10-06T12:56:55+00:00",
  "id": "1234",
  "pages":[
    {
      //Page Object
      "questions": [
        {
          //Question Object
        }
      ]
    }
  ],
  "buttons_text": {
    "done_button": "Done",
    "prev_button": "Prev",
    "exit_button": "Exit",
    "next_button": "Next"
  },
  "footer": true,
  "preview": "https://www.surveymonkey.com/r/Preview/",
  "edit_url": "https://www.surveymonkey.com/create/",
  "collect_url": "https://www.surveymonkey.com/collect/list",
  "analyze_url": "https://www.surveymonkey.com/analyze/",
  "summary_url": "https://www.surveymonkey.com/summary/"
}
```


####Available Methods

 * `GET`: Returns an expanded survey resource with a `pages` element containing a list of all page objects, each containing a list of questions objects. Requires **View Surveys** [scope](#scopes)

###/survey_categories

>Definition

```
GET https://api.surveymonkey.net/v3/survey_categories
```
>Example Request

```shell
curl -i -X GET -H "Authorization:bearer YOUR_ACCESS_TOKEN" -H "Content-Type": "application/json" https://api.surveymonkey.net/v3/survey_categories
```

```python
import requests

s = requests.Session()
s.headers.update({
  "Authorization": "Bearer %s" % YOUR_ACCESS_TOKEN,
  "Content-Type": "application/json"
})

url = "https://api.surveymonkey.net/v3/survey_categories"
s.get(url)
```

>Example Response

```json
{
  "page": 1,
  "per_page": 1,
  "total": 1,
  "data": [{
    "name": "Category Name",
    "id": "community"
  }],
  "links": {
    "self": "https://api.surveymonkey.net/v3/survey_categories?page=1&per_page=1"
  }
}
```

####Available Methods

 * `HEAD`: Checks if resource is available
 * `OPTIONS`: Returns available methods and options
 * `GET`: Returns a list of survey categories that can be used to filter survey templates. Requires **View Library Assets** [scope](#scopes)

####Optional Query Strings for GET

Name | Description | Data Type
------ | ------- | -------
page  | Which page of resources to return. Defaults to 1 | Integer
per_page  | Number of resources to return per page | Integer
language  | ISO 639-1 code for language to filter by (default=en) | String-ENUM

####Survey Categories Resource

Name | Description | Data Type
------ | ------- | -------
data[\_].id | Resource id | String
data[\_].name | Resource name | String


###/survey_templates


>Definition

```
GET https://api.surveymonkey.net/v3/survey_templates
```

>Example Request

```shell
curl -i -X GET -H "Authorization:bearer YOUR_ACCESS_TOKEN" -H "Content-Type": "application/json" https://api.surveymonkey.net/v3/survey_templates?category=all
```

```python
import requests

s = requests.Session()
s.headers.update({
  "Authorization": "Bearer %s" % YOUR_ACCESS_TOKEN,
  "Content-Type": "application/json"
})

payload = {
  "category": "community"
}
url = "https://api.surveymonkey.net/v3/survey_templates"
s.get(url, params=payload)
```

>Example Response

```json
{
  "page": 1,
  "per_page": 1,
  "total": 1,
  "data": [{
    "category": "community",
    "name": "Template Name",
    "title": "Template Name"
    "available": true,
    "id": "49",
    "num_questions":10,
    "description":"Template description",
    "preview_link":"https://www.surveymonkey.com/s.aspx?PREVIEW_MODE=DO_NOT_USE_THIS_LINK_FOR_COLLECTION&sm=ID"
  }],
  "links": {
    "self": "https://api.surveymonkey.net/v3/survey_templates?page=1&per_page=1"
  }
}
```

<aside class="notice"><strong>NOTE for Teams/Groups</strong>: Shared <a href="http://help.surveymonkey.com/articles/en_US/kb/Library/?zip=zip_3">Team templates </a>are not available through the API at this time. This endpoint returns SurveyMonkey's <a href="http://help.surveymonkey.com/articles/en_US/kb/Can-I-create-surveys-from-a-selection-of-survey-templates">template list</a>.</aside>

####Available Methods

 * `HEAD`: Checks if resource is available
 * `OPTIONS`: Returns available methods and options
 * `GET`: Returns a list of survey templates. Survey template ids can be used as an argument to `POST` a new survey. Requires **View Library Assets** [scope](#scopes)

####Optional Query Strings for GET

Name | Description | Data Type
------ | ------- | -------
page | Which page of resources to return. Defaults to 1 | Integer
per_page | Number of resources to return per page | Integer
language | ISO 639-1 code for template language to filter by (default=en) | String-ENUM
category | Category to filter by, see [/survey_categories](#survey_categories) for a list of available categories if not specified, all categories are returned | String-ENUM

####Survey Templates Resource

Name | Description | Type
------ | ------- | -------
data[\_].id | Resource id | String
data[\_].name | Resource name | String
data[\_].title | Survey title | String
data[\_].description | Template description | String
data[\_].category | Template category | String
data[\_].available | Template is available to user | Boolean
data[\_].num_questions | Number of questions in the template | Integer
data[\_].preview_link | Template preview URL | String


###/surveys/{id}/pages

>Definition

```
POST https://api.surveymonkey.net/v3/surveys/{survey_id}/pages
```

>Example Request

```shell
curl -i -X POST -H "Authorization:bearer YOUR_ACCESS_TOKEN" -H "Content-Type": "application/json" https://api.surveymonkey.net/v3/surveys/1234/pages -d '{"title":"Page Title"}'
```

```python
import requests

s = requests.Session()
s.headers.update({
  "Authorization": "Bearer %s" % YOUR_ACCESS_TOKEN,
  "Content-Type": "application/json"
})

payload = {
  "title": "Page Title"
}
url = "https://api.surveymonkey.net/v3/surveys/%s/pages" % (survey_id)
s.post(url, json=payload)
```

>Example Response

```json
{
  "title": "Page Title",
  "description": "",
  "position": 1,
  "question_count": 0,
  "id": "1234",
  "href":"http://api.surveymonkey.com/v3/surveys/1234/pages/1234"
}
```

####Available Methods

 * `HEAD`: Checks if resource is available
 * `OPTIONS`: Returns available methods and options
 * `GET`: Returns a page's details. Requires **View Surveys** [scope](#scopes)
 * `POST`: Creates a new, empty page, see [/surveys/{id}/pages/{id}/questions](#surveys-id-pages-id-questions) to add questions to pages. Requires **Create/Modify Surveys** [scope](#scopes)

####Optional Query Strings for GET

Name | Description | Data Type
------ | ------- | -------
page | Which page of resources to return. Defaults to 1 | Integer
per_page | Number of resources to return per page | Integer

####Page List Resource

Name | Description | Data Type
------ | ------- | -------
data[\_].id | Page ID | String
data[\_].title | Page Title | String
data[\_].description | Page Description | String
data[\_].href | Resource API URL | String
data[\_].position | Position of page in survey | Integer

####Request Body Arguments for POST

Name | Required |Description | Type
------ | ------- |------- | -------
title | No (default="")| Page title | String
description | No (default: "") | Page description | String
position | No (default=end) | Position of page in survey | Integer


###/surveys/{id}/pages/{id}

>Definition

```
GET https://api.surveymonkey.net/v3/surveys/{survey_id}/pages/{page_id}
```

>Example Request

```shell
curl -i -X GET -H "Authorization:bearer YOUR_ACCESS_TOKEN" -H "Content-Type": "application/json" https://api.surveymonkey.net/v3/surveys/1234/pages/1234
```

```python
import requests

s = requests.Session()
s.headers.update({
  "Authorization": "Bearer %s" % YOUR_ACCESS_TOKEN,
  "Content-Type": "application/json"
})

url = "https://api.surveymonkey.net/v3/surveys/%s/pages/%s" % (survey_id, page_id)
s.get(url)
```

>Example Response

```json
{
  "title": "Page Title",
  "description": "",
  "position": 1,
  "question_count": 0,
  "id": "1234",
  "href": "https://api.surveymonkey.com/v3/surveys/1234/pages/1234"
}
```

####Available Methods

 * `HEAD`: Checks if resource is available
 * `OPTIONS`: Returns available methods and options
 * `GET`: Returns a page's details. Requires **View Surveys** [scope](#scopes)
 * `PATCH`: Modifies a page (updates any fields accepted as arguments to `POST` [/surveys{id}/pages](#surveys-id-pages)). Requires **Create/Modify Surveys** [scope](#scopes)
 * `PUT`: Replaces a page (same arguments and requirements as `POST` [/surveys{id}/pages](#surveys-id-pages)). Requires **Create/Modify Surveys** [scope](#scopes)
 * `DELETE`: Deletes a page. Requires **Create/Modify Surveys** [scope](#scopes)

####Request Body Arguments for PUT/PATCH

Name | Required |Description | Data Type
------- | ------- | ------- | -------
title  | No (`PUT` default="") |Page title | String
description | No (`PUT` default="") | Page description | String
position | No (`PUT` default=end) | Page position in survey | String

####Page Resource

Name | Description | Type
------- | ------- | -------
title | Page title | String
description | Page description | String
position | Page position | Integer
question_count | Number of questions on page | Integer
id | Page id | String


