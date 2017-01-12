##Survey Responses

These endpoints let you create responses directly via the API and view responses you have collected through any [collector type](http://help.surveymonkey.com/articles/en_US/kb/How-to-collect-responses).

<aside class="notice"><strong>NOTE for Public Apps</strong>: The View Response Details scope requires An annual paid plan and the Create/Modify Responses scope requires a PLATINUM plan. The View Response Details scope is required for bulk and details endpoints.</aside>


###/surveys/{id}/responses

>Definition

```
GET https://api.surveymonkey.net/v3/surveys/{survey_id}/responses

```

>Example Request

```shell
curl -i -X POST -H "Content-Type: application/json" -H "Authorization:bearer YOUR_ACCESS_TOKEN" https://api.surveymonkey.net/v3/surveys/{survey_id}/responses
```

```python

import requests

s = requests.session()
s.headers.update({
  "Authorization": "Bearer %s" % YOUR_ACCESS_TOKEN,
  "Content-Type": "application/json"
})

url = "https://api.surveymonkey.net/v3/surveys/%s/responses/" % (survey_id)
s.get(url)
```

>Example Response

```json

{
  "per_page": 50,
  "total": 2,
  "data": [
    {
      "href": "https://api.surveymonkey.net/v3/surveys/1234/responses/1234",
      "id": "1234"
    },
    {
      "href": "https://api.surveymonkey.net/v3/surveys/1234/responses/1234",
      "id": "1234"
    }
  ],
  "page": 1,
  "links": {
    "self": "https://api.surveymonkey.net/v3/surveys/1234/responses?page=1&per_page=50"
  }
}


```


####Available Methods

 * `GET`: Returns a list of responses. Requires **View Responses** [scope](#scopes)


###/collectors/{id}/responses

>Definition

```
POST https://api.surveymonkey.net/v3/collectors/{collector_id}/responses
```
>Example Request

```shell
curl -i -X POST -H "Content-Type: application/json" -H "Authorization:bearer YOUR_ACCESS_TOKEN" https://api.surveymonkey.net/v3/surveys/{survey_id}/responses-d '{"custom_variables":{"custvar_1": "one", "custvar_2": "two"},"response_status": "overquota","custom_value": "custom identifier for the response","date_created": "2015-10-06T12:56:55+00:00","ip_address": "127.0.0.1","recipient_id": "564728340", "pages": [{"id": "12345678","questions": [{"answers": [{"choice_id": "12345678"}], "id": "12345678"}, {"answers": [{"row_id": "12345678", "choice_id": "12345678"}], "id": "12345678"}, {"answers": [{"row_id": "12345678", "col_id": "12345678", "choice_id": "12345678"}], "id": "12345678"}, {"answers": [{"text": "Sample Text Response"}], "id": "12345678"}, {"answers": [{"row_id": "12345678", "text": "Sample Text Response"}], "id": "12345678"}]}]}
```

```python
import requests

s = requests.session()
s.headers.update({
  "Authorization": "Bearer %s" % YOUR_ACCESS_TOKEN,
  "Content-Type": "application/json"
})

payload = {
  "custom_variables": {
    "custvar_1": "one",
    "custvar_2": "two"
  },
  "response_status": "completed",
  "custom_value": "custom identifier for the response",
  "date_created": "2015-10-06T12:56:55+00:00",
  "ip_address": "127.0.0.1",
  "recipient_id": "564728340",
{
  "pages": [{
    "id": "12345678",
    "questions": [
    {  ##Single/Multiple Choice
        "answers": [{
            "choice_id": "12345678"
        }],
        "id": "12345678"
    },
    {  ##Matrix Single/Rating/Ranking, Emoji
        "answers": [{
            "row_id": "12345678",
            "choice_id": "12345678"
        }],
        "id": "12345678"
    },
    { ##Matrix Menu
        "answers": [{
            "row_id": "12345678",
            "col_id": "12345678",
            "choice_id": "12345678"
        }],
        "id": "12345678"
    },
    { ##Open Ended Single/Essay, Slider
        "answers": [{
            "text": "Sample Text Response"
        }],
        "id": "12345678"
    },
    { ##Open Ended Multi/Numerical, Demographic, Datetime
        "answers": [{
            "row_id": "12345678",
            "text": "Sample Text Response" ##(format depends on question type, "12/31/2015 11:59 PM" for datetime)
        }],
        "id": "12345678"
    }]
  }]
}
url = "https://api.surveymonkey.net/v3/surveys/%s/responses" % (survey_id)
s.post(url, json=payload)
```

>Example Response to POST request

```json
{
  "total_time": 144,
  "href":"https:\/\/api.surveymonkey.net\/v3\/surveys\/1234\/responses\/1234,
  "ip_address": "192.168.4.16",
  "recipient_id": "",
  "id": "5007154402",
  "logic_path": {},
  "metadata": {},
  "date_modified": "2015-12-28T21:59:38+00:00",
  "response_status": "completed",
  "custom_variables": {
    "custvar_1": "one",
    "custvar_2": "two"
  },
  "edit_url": "https://www.surveymonkey.com/r/",
  "analyze_url": "https://www.surveymonkey.com/analyze/browse/",
  "custom_value": "custom identifier for the response",
  "page_path": [],
  "pages": [{
    "id": "12345678",
    "questions": [
    {"answers": [{
            "choice_id": "12345678"
        }],
        "id": "12345678"
    },
    {"answers": [{
            "row_id": "12345678",
            "choice_id": "12345678"
        }],
        "id": "12345678"
    },
    {"answers": [{
            "row_id": "12345678",
            "col_id": "12345678",
            "choice_id": "12345678"
        }],
        "id": "12345678"
    },
    {"answers": [{
            "text": "Sample Text Response"
        }],
        "id": "12345678"
    },
    { "answers": [{
            "row_id": "12345678",
            "text": "Sample Text Response" ##(format depends on question type, "12/31/2015 11:59 PM" for datetime)
        }],
        "id": "12345678"
    }]
  }],
  "collector_id": "50253690",
  "date_created": "2015-12-28T21:57:14+00:00",
  "survey_id": "105724755",
  "collection_mode": "default"
}
```
####Available Methods

 * `HEAD`: Checks if resource is available
 * `OPTIONS`: Returns available methods and options
 * `GET`: Returns a list of responses. Requires **View Responses** [scope](#scopes)
 * `POST`: Creates a response. Requires **Create/Modify Responses** [scope](#scopes)

####Optional Query Strings for GET

Name | Description | Data Type
------ | ------- | -------
page | Page of resources to return. Defaults to 1 | Integer
per_page | Number of resources to return per page | Integer
start_created_at | Responses started after this date | DateString
end_created_at | Responses started before this date | DateString
start_modified_at | Responses modified after this date | DateString
end_modified_at | Responses modified before this date | DateString
status | Status of the response: `completed`, `partial`, `overquota`, `disqualified` | String-ENUM
email | Email of the recipient | String
first_name | First Name of the recipient | String
last_name | Last Name of the recipient | String
ip | The IP the response was taken from | String
custom | The custom value associated with the response | String
total_time_max | The maximum amount of time spent on the response | Integer
total_time_min | The minimum amount of time spent on the response | Integer
total_time_units | Unit of time for total_time_min and total_time_max: `second`, `minute`, `hour` | String-ENUM
sort_order | Sort order: `ASC` or `DESC`] | String-ENUM
sort_by | Field used to sort returned responses: `date_modified` | String-ENUM

####Response list resources returned from a GET

Name | Description | Data Type
------ | ------- | -------
data[\_].id | Response id | String
data[\_].href | URL for the response resource | String


####Request Body Arguments for POST

Name | Required | Description | Data Type
------ | ------- | ------- | -------
custom_variables | No| Values to any available custom variables in the survey | Object
custom_value | No| A custom value to attach to the response for a [weblink collector](#collectors-id) | String
date_created | No | Date the response was created | DateString
response_status | No | Status of the response: `completed`, `partial`, `overquota`, `disqualified` | String-ENUM
ip_address | No | IP Address the response was taken from | String
recipient_id | No | The recipient ID from an email collector. See [collector recipient](#collectors-id-recipients-id) | Integer
pages | Yes | Pages from the survey and their associated responses | Array
pages[\_].id | Yes | The ID of the page with responses | Integer
pages[\_].questions | Yes | The questions on that page with responses | Array
pages[\_].questions[\_].id | Yes  | ID of the question with responses | Integer
pages[\_].questions[\_].variable_id | No | ID of the random assignment variable for the question | Integer
pages[\_].questions[\_].answers | Yes | The answers for the question with responses. See [formatting question types](#formatting-question-types) | Object
pages[\_].questions[\_].answers[\_].choice_id | No | The choice selected | Integer
pages[\_].questions[\_].answers[\_].row_id | No | The row selected | Integer
pages[\_].questions[\_].answers[\_].col_id | No | The column selected | Integer
pages[\_].questions[\_].answers[\_].other_id | No | The other text choice selected | Integer
pages[\_].questions[\_].answers[\_].text | No| Any open ended text | String


###/surveys/{id}/responses/bulk

Same as [/collectors/{id}/responses/bulk](#collectors-id-responses-bulk)

###/collectors/{id}/responses/bulk

>Definition

```
GET https://api.surveymonkey.net/v3/surveys/{survey_id}/responses/bulk
GET https://api.surveymonkey.net/v3/collectors/{collector_id}/responses/bulk
```

>Example Request

```shell

curl -i -X GET -H "Authorization:bearer YOUR_ACCESS_TOKEN" -H "Content-Type": "application/json" https://api.surveymonkey.net/v3/surveys/{survey_id}/responses/bulk
```

```python
import requests

s = requests.session()
s.headers.update({
  "Authorization": "Bearer %s" % YOUR_ACCESS_TOKEN,
  "Content-Type": "application/json"
})

url = "https://api.surveymonkey.net/v3/surveys/%s/responses/bulk" % (survey_id)
s.get(url, json=payload)
```

>Example Response

```json
{
  "per_page": 2,
  "total": 1,
  "data": [{
    "total_time": 0,
    "collection_mode": "default",
    "href": "https://api.surveymonkey.net/v3/responses/5007154325",
    "custom_variables": {
      "custvar_1": "one",
      "custvar_2": "two"
    },
    "custom_value": "custom identifier for the response",
    "edit_url": "https://www.surveymonkey.com/r/",
    "analyze_url": "https://www.surveymonkey.com/analyze/browse/",
    "ip_address": "",
    "pages": [{
      "id": "103332310",
      "questions": [{
          "answers": [{
              "choice_id": "3057839051"
          }],
          "id": "319352786"
      }]
    }],
    "date_modified": "1970-01-17T19:07:34+00:00",
    "response_status": "completed",
    "id": "5007154325",
    "collector_id": "50253586",
    "recipient_id": "0",
    "date_created": "1970-01-17T19:07:34+00:00",
    "survey_id": "105723396"
  }],
  "page": 1,
  "links": {
    "self": "https://api.surveymonkey.net/v3/surveys/123456/responses/bulk?page=1&per_page=2"
  }
}
```

####Available Methods

 * `GET`: Retrieves a list of full expanded responses, including answers to all questions. Requires **View Response Details** [scope](#scopes)

####Optional Query Strings for GET

Name | Description | Data Type
------ | ------- | -------
page | Page of resources to return. Defaults to 1 | Integer
per_page | Number of resources to return per page. Max of 100 allowed per page. | Integer
collector_ids | Only include responses for this list of collector IDs | Comma Separated Strings
start_created_at | Responses started after this date | DateString
end_created_at | Responses started before this date | DateString
start_modified_at | Responses modified after this date | DateString
end_modified_at | Responses modified before this date | DateString
status | Status of the response: `completed`, `partial`, `overquota`, `disqualified`| String-ENUM
email | Email of the recipient | String
first_name | First Name of the recipient | String
last_name | Last Name of the recipient | String
ip | The IP the response was taken from | String
custom | The custom value associated with the response | String
total_time_max | The maximum amount of time spent on the response | Integer
total_time_min | The minimum amount of time spent on the response | Integer
total_time_units | Unit of time for total_time_min and total_time_max: `second`, `minute`, or `hour` | String-ENUM
sort_order | Sort order: `ASC` or `DESC` | String-ENUM
sort_by | Field used to sort returned responses: `date_modified` | String-ENUM
page_ids | List of survey pages to filter on. Returns all pages if not provided | Commas Seperated Strings
question_ids | List of survey questions to filter on. Returns all questions if not provided | Commas Seperated Strings

####Responses List Resource

Name | Description | Type
------ | ------- | -------
data[\_].id | Response id | String
data[\_].href | URL for the response resource | String
data[\_].survey_id | ID of the survey the response was taken for | String
data[\_].collector_id | ID of the collector the response was taken for | String
data[\_].recipient_id | ID of the recipient (only for email collectors). See [collector recipient](#collectors-id-recipients-id) | String
data[\_].total_time | Total time in seconds spent on the survey | Integer
data[\_].custom_value | Custom value associated with a response | String
data[\_].edit_url | Weblink to the survey taking page to edit the response | String
data[\_].analyze_url | Weblink to the analyze page to view the response | String
data[\_].ip_address | IP Address the response was taken from | String
data[\_].custom_variables | Values to any available custom variables in the survey | Object
data[\_].response_status | Status of the response: `completed`, `partial`, `overquota`, or `disqualified` | String-ENUM
data[\_].collection_mode | The collection mode of the response: `default`, `preview`, `data_entry`, `survey_preview`, or `edit` | String-ENUM
data[\_].date_created | Date the response was created | DateString
data[\_].date_modified | Date the response was last modified  | Object
data[\_].pages | Pages from the survey and their associated responses | Array
data[\_].pages[\_].id | The ID of the page with responses | Integer
data[\_].pages[\_].questions | The questions on that page with responses | Array
data[\_].pages[\_].questions[\_].id | ID of the question with responses | Integer
data[\_].pages[\_].questions[\_].variable_id| ID of the random assignment variable for the question | Integer
data[\_].pages[\_].questions[\_].answers | The answers for the question with responses | List
data[\_].pages[\_].questions[\_].answers[\_].choice_id | The choice selected | Integer
data[\_].pages[\_].questions[\_].answers[\_].row_id | The row selected | Integer
data[\_].pages[\_].questions[\_].answers[\_].col_id | The column selected | Integer
data[\_].pages[\_].questions[\_].answers[\_].other_id | The other text choice selected | Integer
data[\_].pages[\_].questions[\_].answers[\_].text | Any open ended text | String



###/surveys/{id}/responses/{id}

Same as [/collectors/{id}/responses/{id}](#collectors-id-responses-id)

###/collectors/{id}/responses/{id}

>Definition

```
GET https://api.surveymonkey.net/v3/surveys/{survey_id}/responses/{response_id}
GET https://api.surveymonkey.net/v3/collectors/{collector_id}/responses/{response_id}
```

>Example Request

```shell

curl -i -X GET -H "Authorization:bearer YOUR_ACCESS_TOKEN" -H "Content-Type": "application/json" https://api.surveymonkey.net/v3/surveys/{survey_id}/responses/{response_id}
```

```python
import requests

s = requests.session()
s.headers.update({
  "Authorization": "Bearer %s" % YOUR_ACCESS_TOKEN,
  "Content-Type": "application/json"
})

url = "https://api.surveymonkey.net/v3/surveys/%s/responses/%s" % (survey_id, response_id)
s.get(url)
```

>Example Response

```json
{
  "total_time": 144,
  "ip_address": "192.168.4.16",
  "recipient_id": "",
  "id": "5007154402",
  "logic_path": {},
  "metadata": {},
  "date_modified": "2015-12-28T21:59:38+00:00",
  "response_status": "completed",
  "custom_variables": {
    "custvar_1": "one",
    "custvar_2": "two"
  },
  "custom_value": "custom identifier for the response",
  "edit_url": "https://www.surveymonkey.com/r/",
  "analyze_url": "https://www.surveymonkey.com/analyze/browse/",
  "page_path": [],
  "collector_id": "50253690",
  "date_created": "2015-12-28T21:57:14+00:00",
  "survey_id": "105724755",
  "collection_mode": "default"
}
```

####Available Methods

 * `HEAD`: Checks if resource is available
 * `OPTIONS`: Returns available methods and options
 * `GET`: Returns a response. Requires **View Responses** [scope](#scopes)
 * `PATCH`: Modifies a response (updates any fields accepted as arguments to `POST` [/surveys/{id}/responses](#surveys-id-responses)). Requires **Create/Modify Responses** [scope](#scopes)
 * `PUT`: Replaces a response (same arguments and requirements as `POST` [/surveys/{id}/responses](#surveys-id-responses)). Requires **Create/Modify Responses** [scope](#scopes)
 * `DELETE`: Deletes a response, Requires **Create/Modify Responses** [scope](#scopes)

####Response Resource

Name | Description | Type
------ | ------- | -------
survey_id | ID of the survey the response was taken for | String
collector_id | ID of the collector the response was taken for | String
recipient_id | ID of the recipient (only for email collectors). See [collector recipient](#collectors-id-recipients-id) | String
total_time | Total time in seconds spent on the survey | Integer
custom_value | Custom value associated with a response | String
edit_url | Weblink to the survey taking page to edit the response | String
analyze_url | Weblink to the analyze page to view the response | String
ip_address | IP Address the response was taken from | String
custom_variables | Values to any available custom variables in the survey | Object
logic_path | Logic path taken during the survey | Object
metadata | Other associated metadata or custom values | Object
response_status | Status of the response: `completed`, `partial`, `overquota`, or `disqualified` | String-ENUM
page_path | The order in which the pages were responded to. | Array
collection_mode | The collection mode of the response: `default`, `preview`, `data_entry`, `survey_preview`, or `edit` | String-ENUM
date_created | Date the response was created | DateString
date_modified | Date the response was last modified  | DateString



###/surveys/{id}/responses/{id}/details

Same as [/collectors/{id}/responses/{id}/details](#collectors-id-responses-id-details)

###/collectors/{id}/responses/{id}/details

>Definition

```
GET https://api.surveymonkey.net/v3/surveys/{survey_id}/responses/{response_id}/details
GET https://api.surveymonkey.net/v3/collectors/{collector_id}/responses/{response_id}/details
```

>Example Request

```shell

curl -i -X GET -H "Authorization:bearer YOUR_ACCESS_TOKEN" -H "Content-Type": "application/json" https://api.surveymonkey.net/v3/surveys/{survey_id}/responses/{response_id}/details
```

```python
import requests

s = requests.session()
s.headers.update({
  "Authorization": "Bearer %s" % YOUR_ACCESS_TOKEN,
  "Content-Type": "application/json"
})

url = "https://api.surveymonkey.net/v3/surveys/%s/responses/%s/details" % (survey_id, response_id)
s.get(url)
```

>Example Response

```json
{
  "total_time": 144,
  "ip_address": "192.168.4.16",
  "recipient_id": "",
  "id": "5007154402",
  "logic_path": {},
  "metadata": {},
  "date_modified": "2015-12-28T21:59:38+00:00",
  "response_status": "completed",
  "custom_variables": {
    "custvar_1": "one",
    "custvar_2": "two"
  },
  "custom_value": "custom identifier for the response",
  "edit_url": "https://www.surveymonkey.com/r/",
  "analyze_url": "https://www.surveymonkey.com/analyze/browse/",
  "page_path": [],
  "pages": [{
    "id": "103332310",
    "questions": [{
        "answers": [{
            "choice_id": "3057839051"
        }],
        "id": "319352786"
    }]
  }],
  "collector_id": "50253690",
  "date_created": "2015-12-28T21:57:14+00:00",
  "survey_id": "105724755",
  "collection_mode": "default"
}
```

####Available Methods

 * `GET`: Retrieve a full expanded response, including answers to all questions. Requires **View Response Details** [scope](#scopes)

####Optional Query Strings for GET

Name | Description | Data Type
------ | ------- | -------
page_ids | List of survey pages to filter on. Returns all pages if not provided | Commas Seperated Strings
question_ids | List of survey questions to filter on. Returns all questions if not provided | Commas Seperated Strings


####Response Resource

Name | Description | Type
------ | ------- | -------
survey_id | ID of the survey the response was taken for | String
collector_id | ID of the collector the response was taken for | String
recipient_id | ID of the recipient (only for email collectors). See [collector recipient](#collectors-id-recipients-id) | String
total_time | Total time in seconds spent on the survey | Integer
custom_value | Custom value associated with a response | String
edit_url | Weblink to the survey taking page to edit the response | String
analyze_url | Weblink to the analyze page to view the response | String
ip_address | IP Address the response was taken from | String
custom_variables | Values to any available custom variables in the survey | Object
logic_path | Logic path taken during the survey | Object
metadata | Other associated metadata or custom values | Object
response_status | Status of the response: `completed`, `partial`, `overquota`, or `disqualified` | String-ENUM
current_page_id |  ID of the page the respondent is currently on, "0" if completed | String
page_path | The order in which the pages were responded to. | Array
collection_mode | The collection mode of the response: `default`, `preview"`, `data_entry`, `survey_preview`, or `edit`| String-ENUM
date_created | Date the response was created | DateString
date_modified | Date the response was last modified  | DateString
pages | Pages from the survey and their associated responses | Array
pages[\_].id | The ID of the page with responses | Integer
pages[\_].questions | The questions on that page with responses | Array
pages[\_].questions[\_].id | ID of the question with responses | Integer
pages[\_].questions[\_].variable_id | ID of the random assignment variable for the question | Integer
pages[\_].questions[\_].answers | The answers for the question with responses | List
pages[\_].questions[\_].answers[\_].choice_id | The choice selected | Integer
pages[\_].questions[\_].answers[\_].row_id | The row selected | Integer
pages[\_].questions[\_].answers[\_].col_id | The column selected | Integer
pages[\_].questions[\_].answers[\_].other_id | The other text choice selected | Integer
pages[\_].questions[\_].answers[\_].text | Any open ended text | String
