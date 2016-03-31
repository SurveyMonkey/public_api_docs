##Survey Responses

These endpoints let you create responses directly via the API and view responses you have collected through any [collector type](http://help.surveymonkey.com/articles/en_US/kb/How-to-collect-responses).

[Scopes](#scopes) to use some of these endpoints require a [paid plan](https://www.surveymonkey.com/pricing/?ut_source=dev_portal&amp;ut_source2=docs"). The View Response Details scope requires A GOLD plan and the Create/Modify Responses scope requires ENTERPRISE/PLATINUM plan. The View Response Details scope is required for bulk and details endpoints.


###/surveys/{id}/responses

####Available Methods

 * `GET`: Returns a list of responses in same format as `GET` to [/collectors/{id}/responses]()


###/collectors/{id}/responses

>Definition

```
POST https://api.surveymonkey.net/v3/collectors/{collector_id}/responses
```
>Example Request

```shell
curl -i -X POST -H "Authorization:bearer YOUR_ACCESS_TOKEN" https://api.surveymonkey.net/v3/surveys/{survey_id}/responses?api_key=YOUR_API_KEY -d '{"type":"weblink"}'
```

```python
import requests

s = requests.session()

payload = {
  "custom_variables": {
    "custvar_1": "one",
    "custvar_2": "two"
  },
  "date_created": "2015-10-06T12:56:55+00:00",
  "ip_address": "127.0.0.1",
  "recipient_id": "564728340",
  "pages": [{
    "id": "103332310",
    "questions": [{
        "answers": [{
            "choice_id": "3057839051"
        }],
        "id": "319352786"
    }]
  }]
}
url = "https://api.surveymonkey.net/v3/surveys/%s/responses?api_key=%s" % (survey_id, YOUR_API_KEY)
s.post(url, data=payload)
```

>Example Response

```json
{
  "per_page": 2,
  "data": [{
    "id": "12345678",
    "href": "https://api.surveymonkey.net/v3/surveys/%s/responses/12345678"
  }],
  "page": 1
}
```
####Available Methods

 * `HEAD`: Checks if resource is available
 * `OPTIONS`: Returns available methods and options
 * `GET`: Returns a list of responses
 * `POST`: Creates a response

####Optional Query Strings for GET

Name | Description | Type
------ | ------- | -------
page | Page of resources to return. Defaults to 1 | Integer
per_page | Number of resources to return per page | Integer
start_created_at | Responses started after this date | Date String
end_created_at | Responses started before this date | Date String
start_modified_at | Responses modified after this date | Date String
end_modified_at | Responses modified before this date | Date String
status | Status of the response ['completely', 'partially', 'overquota', 'disqualified'] | String-ENUM
email | Email of the recipient | String
first_name | First Name of the recipient | String
last_name | Last Name of the recipient | String
ip | The IP the response was taken from | String
custom | The custom value associated with the response | String
total_time_max | The maximum amount of time spent on the response | Integer
total_time_min | The minimum amount of time spent on the response | Integer
total_time_units | Unit of time for total_time_min and total_time_max ['second', 'minute', 'hour'] | String-ENUM
sort_order | Sort order: 'ASC' or 'DESC'] | String-ENUM
sort_by | Field used to sort returned responses ['date_modified'] | String-ENUM

####Response list resources

Name | Description | Type
------ | ------- | -------
data.id | Response id | String
data.href | URL for the response resource | String


####Request Body Arguments for POST

Name | Required | Description | Type
------ | ------- | ------- | -------
custom_variables | No| Values to any available custom variables in the survey | Object
date_created | No | Date the response was created | Date String
ip_address | No | IP Address the response was taken from | String
recipient_id | No | The recipient ID from an email collector | Integer
pages | Yes | Pages from the survey and their associated responses | Array
pages[_].id | Yes | The ID of the page with responses | Integer
pages[_].questions | Yes | The questions on that page with responses | Array
pages[\_].questions[_].id | Yes  | ID of the question with responses | Integer
pages[\_].questions[\_].variable_id | No | ID of the random assignment variable for the question | Integer
pages[\_].questions[\_].answers | Yes | The answers for the question with responses. See [formatting question types](#formatting-question-types) | List
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

curl -i -X GET -H "Authorization:bearer YOUR_ACCESS_TOKEN" https://api.surveymonkey.net/v3/surveys/{survey_id}/responses/bulk?api_key=YOUR_API_KEY
```

```python
import requests

s = requests.session()

payload = {
  "page": 1,
  "per_page": 2,
  "start_created_at": "2015-10-06T12:56:55+00:00",
  "end_created_at": "2015-10-06T12:56:55+00:00",
  "status": "completely",
  "email": "test@surveymonkey.com",
  "first_name": "Jon",
  "last_name": "Doe",
  "ip": "127.0.0.1",
  "custom": "custom value",
  "total_time_max": 10000,
  "total_time_min": 1000,
  "total_time_units": "second",
  "sort_order": "ASC",
  "sort_by": "date_modified"
}
url = "https://api.surveymonkey.net/v3/surveys/%s/responses/bulk?api_key=%s" % (survey_id, YOUR_API_KEY)
s.get(url, params=payload)
```

>Example Response

```json
{
  "per_page": 2,
  "data": [{
    "total_time": 0,
    "collection_mode": "normal",
    "href": "https://api.surveymonkey.net/v3/responses/5007154325",
    "custom_variables": {
      "custom1": "MyValue"
    },
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
    "custom_value": "",
    "id": "5007154325",
    "collector_id": "50253586",
    "recipient_id": "0",
    "date_created": "1970-01-17T19:07:34+00:00",
    "survey_id": "105723396"
  }],
  "page": 1
}
```

####Available Methods

 * `GET`: Retrieves a list of full expanded responses, including answers to all questions

####Optional Query Strings for GET

Name | Description | Type
------ | ------- | -------
page | Page of resources to return. Defaults to 1 | Integer
per_page | Number of resources to return per page | Integer
collector_ids | Only include responses for this list of collector IDs | Comma Separated List
start_created_at | Responses started after this date | Date String
end_created_at | Responses started before this date | Date String
start_modified_at | Responses modified after this date | Date String
end_modified_at | Responses modified before this date | Date String
status | Status of the response ['completely', 'partially', 'overquota', 'disqualified'] | String-ENUM
email | Email of the recipient | String
first_name | First Name of the recipient | String
last_name | Last Name of the recipient | String
ip | The IP the response was taken from | String
custom | The custom value associated with the response | String
total_time_max | The maximum amount of time spent on the response | Integer
total_time_min | The minimum amount of time spent on the response | Integer
total_time_units | Unit of time for total_time_min and total_time_max: 'second', 'minute', or 'hour' | String-ENUM
sort_order | Sort order: 'ASC' or 'DESC'] | String-ENUM
sort_by | Field used to sort returned responses ['date_modified'] | String-ENUM

####Responses List Resource

Name | Description | Type
------ | ------- | -------
data.id | Response id | String
data.href | URL for the response resource | String
data.survey_id | ID of the survey the response was taken for | String
data.collector_id | ID of the collector the response was taken for | String
data.recipient_id | ID of the recipient (only for email collectors) | String
data.total_time | Total time in seconds spent on the survey | Integer
data.last_name | Last name of the recipient (if recipient ID was provided) | String
data.custom_value | Custom value associated with a recipient | String
data.ip_address | IP Address the response was taken from | String
data.custom_variables | Values to any available custom variables in the survey | Object
response_status | Status of the response: "completed", "new", "overquota", or "disqualified" | String
collection_mode | The collection mode of the response: "default", "preview", "data_entry", "survey_preview", or "edit" | Object
data.date_created | Date the response was created | Date String
data.date_modified | Date the response was last modified  | Object
data.pages | Pages from the survey and their associated responses | Array
data.pages[\_].id | The ID of the page with responses | Integer
data.pages[\_].questions | The questions on that page with responses | Array
data.pages[\_].questions[\_].id | ID of the question with responses | Integer
data.pages[\_].questions[\_].variable_id| ID of the random assignment variable for the question | Integer
data.pages[\_].questions[\_].answers | The answers for the question with responses | List
data.pages[\_].questions[\_].answers[\_].choice_id | The choice selected | Integer
data.pages[\_].questions[\_].answers[\_].row_id | The row selected | Integer
data.pages[\_].questions[\_].answers[\_].col_id | The column selected | Integer
data.pages[\_].questions[\_].answers[\_].other_id | The other text choice selected | Integer
data.pages[\_].questions[\_].answers[\_].text | Any open ended text | String



###/responses/{id}

>Definition

```
GET https://api.surveymonkey.net/v3/responses/{response_id}
```

>Example Request

```shell

curl -i -X GET -H "Authorization:bearer YOUR_ACCESS_TOKEN" https://api.surveymonkey.net/v3/responses/{response_id}?api_key=YOUR_API_KEY
```

```python
import requests

s = requests.session()

url = "https://api.surveymonkey.net/v3/responses/%s?api_key=%s" % (response_id, YOUR_API_KEY)
s.get(url)
```

>Example Response

```json
{
  "total_time": 144,
  "survey_completed": true,
  "ip_address": "192.168.4.16",
  "recipient_id": "0",
  "email_address": "",
  "id": "5007154402",
  "logic_path": {},
  "metadata": {},
  "date_modified": "2015-12-28T21:59:38+00:00",
  "response_status": "completed",
  "custom_value": "",
  "current_page_id": "0",
  "page_path": [],
  "collector_id": "50253690",
  "survey_version": 17,
  "date_created": "2015-12-28T21:57:14+00:00",
  "survey_id": "105724755",
  "collection_mode": "default"
}
```

####Available Methods

 * `HEAD`: Checks if resource is available
 * `OPTIONS`: Returns available methods and options
 * `GET`: Returns a response
 * `PATCH`: Modifies a response (updates any fields accepted as arguments to `POST` [/responses](#responses))
 * `PUT`: Replaces a response (same arguments and requirements as `POST` [/responses](#responses))
 * `DELETE`: Deletes a response

####Response Resource

Name | Description | Type
------ | ------- | -------
survey_id | ID of the survey the response was taken for | String
collector_id | ID of the collector the response was taken for | String
recipient_id | ID of the recipient (only for email collectors) | String
total_time | Total time in seconds spent on the survey | Integer
last_name | Last name of the recipient (if recipient ID was provided) | String
custom_value | Custom value associated with a recipient | String
survey_completed | Whether or not the the survey is completed | Boolean
ip_address | IP Address the response was taken from | String
custom_variables | Values to any available custom variables in the survey | Object
email_address | Email address associated with a recipient | String
logic_path | Logic path taken during the survey | Object
metadata | Other associated metadata or custom values | Object
first_name | First name associated with a recipient | String
response_status | Status of the response: "completed", "new", "overquota", or "disqualified" | String
current_page_id |  ID of the page the respondent is currently on, "0" if completed | String
page_path | The order in which the pages were responded to. | Array
survey_version | The version of the survey the response was taken for | Integer
collection_mode | The collection mode of the response: "default", "preview", "data_entry", "survey_preview", or "edit" | Object
date_created | Date the response was created | Date String
date_modified | Date the response was last modified  | Object


###/responses/{id}/details

>Definition

```
GET https://api.surveymonkey.net/v3/responses/{response_id}/details
```

>Example Request

```shell

curl -i -X GET -H "Authorization:bearer YOUR_ACCESS_TOKEN" https://api.surveymonkey.net/v3/responses/{response_id}/details?api_key=YOUR_API_KEY
```

```python
import requests

s = requests.session()

url = "https://api.surveymonkey.net/v3/responses/%s/details?api_key=%s" % (response_id, YOUR_API_KEY)
s.get(url)
```

>Example Response

```json
{
  "total_time": 144,
  "survey_completed": true,
  "ip_address": "192.168.4.16",
  "recipient_id": "0",
  "email_address": "",
  "id": "5007154402",
  "logic_path": {},
  "metadata": {},
  "date_modified": "2015-12-28T21:59:38+00:00",
  "response_status": "completed",
  "custom_value": "",
  "current_page_id": "0",
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
  "survey_version": 17,
  "date_created": "2015-12-28T21:57:14+00:00",
  "survey_id": "105724755",
  "collection_mode": "default"
}
```

####Available Methods

 * `GET`: Retrieve a full expanded response, including answers to all questions

####Response Resource

Name | Description | Type
------ | ------- | -------
survey_id | ID of the survey the response was taken for | String
collector_id | ID of the collector the response was taken for | String
recipient_id | ID of the recipient (only for email collectors) | String
total_time | Total time in seconds spent on the survey | Integer
last_name (Required) | Last name of the recipient (if recipient ID was provided) | String
custom_value | Custom value associated with a recipient | String
survey_completed  | Whether or not the the survey is completed | Boolean
ip_address | IP Address the response was taken from | String
custom_variables | Values to any available custom variables in the survey | Object
email_address | Email address associated with a recipient | String
logic_path | Logic path taken during the survey | Object
metadata | Other associated metadata or custom values | Object
first_name | First name associated with a recipient | String
response_status | Status of the response: "completed", "new", "overquota", or "disqualified" | String
current_page_id |  ID of the page the respondent is currently on, "0" if completed | String
page_path | The order in which the pages were responded to. | Array
survey_version | The version of the survey the response was taken for | Integer
collection_mode| The collection mode of the response: "default", "preview", "data_entry", "survey_preview", or "edit"| Object
date_created | Date the response was created | Date String
date_modified | Date the response was last modified  | Object
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
