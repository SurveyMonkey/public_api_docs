##Surveys, Pages, and Questions

The following endpoints let you create surveys, survey pages, and add questions to survey pages. 

A POST to /surveys will create an empty survey to which you can add [pages](#surveys-id-pages) and [questions](#surveys-id-pages-id-questions) (See [formatting question types](#formatting-question-types)). This endpoint also accepts a survey or template ID as an arguement to create a pre-populated survey that can be used as is or modified by deleting, updating, or adding pages or questions. 

A survey needs at least one page and question in order to record a survey [response](#surveys-id-responses). 

<aside class="notice">strong>NOTE for Public Apps</strong>: The View Surveys scope is available on the BASIC (Free) plan and the Create/Modify Surveys scope requires a <a href="https://www.surveymonkey.com/pricing/?ut_source=dev_portal&amp;ut_source2=docs">SELECT plan</a>.</aside>
 

###/surveys

>Definition

```
POST https://api.surveymonkey.net/v3/surveys
```


>Example Request

```shell
curl -i -X POST -H "Authorization:bearer YOUR_ACCESS_TOKEN" https://api.surveymonkey.net/v3/surveys?api_key=YOUR_API_KEY -d '{"title":"My Survey"}'
```

```python
import requests

s = requests.Session()

payload = {
  "title": "My Survey"
}
url = "https://api.surveymonkey.net/v3/surveys?api_key=%s" % YOUR_API_KEY
s.post(url, data=payload)
```
>Example Response

```json
{
  "title": "My Survey",
  "custom_variables": ["custom_variable"],
  "language": "en",
  "question_count": 10,
  "page_count": 10,
  "date_created": "2015-10-06T12:56:55+00:00",
  "date_modified": "2015-10-06T12:56:55+00:00",
  "id": "1234",
  "href":"http://api.surveymonkey.com/v3/surveys/1234",
  "buttons_text": {
    "done_button": "Done",
    "prev_button": "Prev",
    "exit_button": "Exit",
    "next_button": "Next"
  }
}
```

####Available Methods

 * `HEAD`: Checks if resource is available
 * `OPTIONS`: Returns available methods and options
 * `GET`: Returns a list of surveys owned or shared with the authenticated user
 * `POST`: Creates a new empty survey or, if a [template](#survey_templates) id or an existing survey id is specified, a survey prepopulated with [pages](#surveys-id-pages) and [questions](#formatting-question-types)

####Optional Query Strings for GET

Name | Description | Type
------ | ------- | -------
page | Which page of resources to return. Defaults to 1 | Integer
per_page | Number of resources to return per page | Integer
sort_by | Field used to sort returned survey list: 'title', 'date_modified', or 'num_responses' | String-ENUM
sort_order | Sort order: 'ASC' or 'DESC' | String-ENUM
include | Collaboration option to filter survey list: 'shared_with', 'shared_by', or 'owned' | String-ENUM
start_modified_at | Surveys must be last modified after this date. | Date String
end_modified_at | Surveys must be last modified before this date. | Date String

####Survey List Resource

Name | Description | Type
------ | ------- | -------
data.id | Survey id | String
data.title | Survey title | String
data.href | Resource API URL | String

####Request Body Arguments for POST

Name |Required| Description | Type
------ | ----- | ------- | -------
title | No (default="New Survey")|Survey title | String
from_template_id | No | Survey template to copy from. See [/survey_templates](#survey_templates) | String
language | No (default="en") | Survey language | String
buttons_text | No | Survey Buttons text container | Objects
buttons_text.next_button | No | Button text | String
buttons_text.prev_button | No | Button text | String
buttons_text.exit_button | No | Button text | String
buttons_text.done_button | No | Button text | String

####Request Body Arguments for Bulk POST

Name | Required | Description | Type
------ | ----- | ------- | -------
title | No (default="New Survey")|Survey title | String
language | No (default="en") | Survey language | String
buttons_text | No | Survey Buttons text container | Objects
buttons_text.next_button | No | Button text | String
buttons_text.prev_button | No | Button text | String
buttons_text.exit_button | No | Button text | String
buttons_text.done_button | No | Button text | String
pages | Yes | Pages to be created | List of Page Objects
pages[_].questions | Yes | Questions to be created | List of Question Objects


###/surveys/{id}

>Definition

```
GET https://api.surveymonkey.net/v3/surveys/{survey_id}
```

>Example Request

```shell
curl -i -X GET -H "Authorization:bearer YOUR_ACCESS_TOKEN" https://api.surveymonkey.net/v3/surveys/1234?api_key=YOUR_API_KEY
```

```python
import requests

s = requests.Session()

url = "https://api.surveymonkey.net/v3/surveys/%s?api_key=%s" % (survey_id, YOUR_API_KEY)
s.get(url)
```
>Example Response

```json
{
  "title": "My Survey",
  "custom_variables": [],
  "language": "en",
  "question_count": 0,
  "page_count": 0,
  "date_created": "2015-10-06T12:56:55+00:00",
  "date_modified": "2015-10-06T12:56:55+00:00",
  "id": "1234",
  "href": "http://api.surveymonkey.com/v3/surveys/1234",
  "buttons_text": {
    "done_button": "Done",
    "prev_button": "Prev",
    "exit_button": "Exit",
    "next_button": "Next"
  }
}
```
####Available Methods

 * `HEAD`: Checks if resource is available
 * `OPTIONS`: Returns available methods and options
 * `GET`: Returns a survey's details. To get an expanded version showing all pages and questions use [/surveys/{survey_id}/details](#surveys-id-details)
 * `PATCH`: Modifies a survey's title or language
 * `PUT`:  Replaces a survey. Request body arguments the same as POST [/surveys](#surveys)
 * `DELETE`: Deletes a survey

####Request Body Arguments for PATCH (See POST [/surveys](#surveys) for PUT arguments)

Name | Required | Description | Type
------ | ----- | ------- | -------
title | No (`PUT` default="New Survey") |Survey title | String
language | No (`PUT` default="en") | Survey language | String
buttons_text | No | Survey Buttons text container | Objects
buttons_text.next_button | No | Button text | String
buttons_text.prev_button | No | Button text | String
buttons_text.exit_button | No | Button text | String
buttons_text.done_button | No | Button text | String

####Survey Resource

Name | Description | Type
------ | ------- | -------
id | Survey id | String
title | Survey title | String
custom_variables | List of survey variables | Array
language | Survey language | String
question_count | Number of questions in survey | Integer
page_count | Number of pages in survey | Integer
date_created | Date and time when survey was created | Date String
date_modified | Date and time when survey was last modified | Date String
buttons_text.next_button | Button text | String
buttons_text.prev_button | Button text | String
buttons_text.exit_button | Button text | String
buttons_text.done_button | Button text | String
href | Resource API URL | String


###/surveys/{id}/details

>Definition

```
GET https://api.surveymonkey.net/v3/surveys/{survey_id}/details
```

>Example Request

```shell
curl -i -X GET -H "Authorization:bearer YOUR_ACCESS_TOKEN" https://api.surveymonkey.net/v3/surveys/1234/details?api_key=YOUR_API_KEY
```

```python
import requests

s = requests.Session()

url = "https://api.surveymonkey.net/v3/surveys/%s/details?api_key=%s" % (survey_id, YOUR_API_KEY)
s.get(url)
```

>Example Response

```json
{
  "title": "My Survey",
  "custom_variables": ["custom_variable"],
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
  ]
}
```


####Available Methods

 * `GET`: Returns an expanded survey resource with a `pages` element containing a list of all page objects, each containing a list of questions objects

###/survey_categories

>Definition

```
GET https://api.surveymonkey.net/v3/survey_categories
```
>Example Request

```shell
curl -i -X GET -H "Authorization:bearer YOUR_ACCESS_TOKEN" https://api.surveymonkey.net/v3/survey_categories?api_key=YOUR_API_KEY
```

```python
import requests

s = requests.Session()

url = "https://api.surveymonkey.net/v3/survey_categories" % YOUR_API_KEY
s.get(url)
```

>Example Response

```json
{
  "page": 1,
  "per_page": 1,
  "data": [{
    "name": "Category Name",
    "id": "community"
  }]
}
```

####Available Methods

 * `HEAD`: Checks if resource is available
 * `OPTIONS`: Returns available methods and options
 * `GET`: Returns a list of survey categories that can be used to filter survey templates

####Optional Query Strings for GET

Name | Description | Type
------ | ------- | -------
page  | Which page of resources to return. Defaults to 1 | Integer
per_page  | Number of resources to return per page | Integer
language  | Category language to filter by (default=en) | String-ENUM

####Survey Categories Resource

Name | Description | Type
------ | ------- | -------
data[_].id | Resource id | String
data[_].name | Resource name | String


###/survey_templates


>Definition

```
GET https://api.surveymonkey.net/v3/survey_templates
```

>Example Request

```shell
curl -i -X GET -H "Authorization:bearer YOUR_ACCESS_TOKEN" https://api.surveymonkey.net/v3/survey_templates?api_key=YOUR_API_KEY&category=all
```

```python
import requests

s = requests.Session()

payload = {
  "category": "community"
}
url = "https://api.surveymonkey.net/v3/survey_templates" % YOUR_API_KEY
s.get(url, params=payload)
```

>Example Response

```json
{
  "page": 1,
  "per_page": 1,
  "data": [{
    "category": "community",
    "name": "Template Name",
    "available": true,
    "id": "49"
  }]
}
```

####Available Methods

 * `HEAD`: Checks if resource is available
 * `OPTIONS`: Returns available methods and options
 * `GET`: Returns a list of survey templates. Survey template ids can be used as an argument to `POST` a new survey

####Optional Query Strings for GET

Name | Description | Type
------ | ------- | -------
page | Which page of resources to return. Defaults to 1 | Integer
per_page | Number of resources to return per page | Integer
language | Template language to filter by (default=en) | String-ENUM
category | Category to filter by, see [/survey_categories](#survey_categories) for a list of available categories if not specified, all categories are returned | String-ENUM

####Survey Templates Resource

Name | Description | Type
------ | ------- | -------
data[_].id (Required) | Resource id | String
data[_].name (Required) | Resource name | String
data[_].category (Required) | Template Category | String
data[_].available (Required) | Template is availabel to user | Boolean


###/surveys/{id}/pages

>Definition

```
POST https://api.surveymonkey.net/v3/surveys/{survey_id}/pages
```

>Example Request

```shell
curl -i -X POST -H "Authorization:bearer YOUR_ACCESS_TOKEN" https://api.surveymonkey.net/v3/surveys/1234/pages?api_key=YOUR_API_KEY -d '{"title":"Page Title"}'
```

```python
import requests

s = requests.Session()

payload = {
  "title": "Page Title"
}
url = "https://api.surveymonkey.net/v3/surveys/%s/pages" % (survey_id, YOUR_API_KEY)
s.post(url, data=payload)
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
 * `GET`: Returns a page's details
 * `POST`: Creates a new, empty page, see [/surveys/{id}/pages/{id}/questions](#surveys-id-pages-id-questions) to add questions to pages

####Optional Query Strings for GET

Name | Description | Type
------ | ------- | -------
page | Which page of resources to return. Defaults to 1 | Integer
per_page | Number of resources to return per page | Integer

####Page Resource

Name | Description | Type
------ | ------- | -------
data.id | Page ID | String
data.title | Page Title | String
data.description | Page Description | String
data.href | Resource API URL | String
data.position | Position of page in survey | Integer
data.question_count | Number of questions on the page | Integer

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
curl -i -X GET -H "Authorization:bearer YOUR_ACCESS_TOKEN" https://api.surveymonkey.net/v3/surveys/1234/pages/1234?api_key=YOUR_API_KEY
```

```python
import requests

s = requests.Session()

url = "https://api.surveymonkey.net/v3/surveys/%s/pages/%s" % (survey_id, page_id, YOUR_API_KEY)
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
 * `GET`: Returns a page's details
 * `PATCH`: Modifies a page (updates any fields accepted as arguments to `POST` [/surveys{id}/pages](#surveys-id-pages))
 * `PUT`: Replaces a page (same arguments and requirements as `POST` [/surveys{id}/pages](#surveys-id-pages))
 * `DELETE`: Deletes a page

####Request Body Arguments for PUT/PATCH

Name | Required |Description | Type
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


