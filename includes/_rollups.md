##Response Counts and Trends

The following endpoints let you view how many respondents answered a question a particular way and trends in how many respondents answered a question a particular way in a given time period, for example a week.

<aside class="notice">Trends are not available for file_upload, slider, presentation, demographic, matrix_menu, or datetime question types and trends object will return empty for these questions.</aside>

###/surveys/{id}/rollups

>Definition

```
GET https://api.surveymonkey.net/v3/surveys/{id}/rollups
```

>Example Request

```shell
curl -i -X GET -H "Authorization:bearer YOUR_ACCESS_TOKEN" -H "Content-Type": "application/json" https://api.surveymonkey.net/v3/surveys/1234/rollups'
```

```python
import requests

s = requests.Session()
s.headers.update({
  "Authorization": "Bearer %s" % YOUR_ACCESS_TOKEN,
  "Content-Type": "application/json"
})

url = "https://api.surveymonkey.net/v3/surveys/%s/rollups" % (survey_id)
s.get(url)
```
>Example Response

```json

{
   "per_page":50,
   "total":2,
   "data":[
      {
         "subtype":"essay",
         "href":"https://api.surveymonkey.net/v3/surveys/1234/pages/1234/questions/1234/rollups",
         "id":"1234",
         "family":"essay",
         "summary":[
            {
               "answered":3,
               "skipped":1,
               "other_answered":0,
               "text":0
            }
         ]
      },
      {
         "subtype":"vertical",
         "href":"https://api.surveymonkey.net/v3/surveys/1234/pages/1234/questions/1234/rollups",
         "id":"1234",
         "family":"single_choice",
         "summary":[
            {
               "answered":0,
               "skipped":0,
               "stats":{
                  "std":0,
                  "max":0,
                  "min":0,
                  "median":0,
                  "mean":0
               },
               "other_answered":0,
               "choices":[
                  {
                     "count":0,
                     "id":"1234"
                  }
               ]
            }
         ]
      }
   ],
   "page":1,
   "links":{
      "self":"https:\/\/api.surveymonkey.net/v3/surveys/1234/rollups?page=1&per_page=50"
   }
}



```

####Available Methods

 * `HEAD`: Checks if resource is available
 * `OPTIONS`: Returns available methods and options
 * `GET`: Returns rollups for all questions in a survey. Public App users need access to the **View Response Details** [scope](#scopes)

####Optional Query Strings for GET

Name | Description | Data Type
------ | ------- | -------
collector_ids|Limits responses to those from specified collector ids|Comma separated strings 
start_created_at|Limits responses to those created after date specified|Date string
end_created_at|Limits responses to those created before date specified|Date string
start_modified_at|Limits responses to those last modified after date specified|Date string in format YYYY-MM-DDTHH:MM:SS (no offset)
end_modified_at|Limits responses to those last modified before date specified|Date string in format YYYY-MM-DDTHH:MM:SS (no offset)
status|Limits responses to those of a certain status. Accepts: `completed`, `partial`, `overquota`, `disqualified`|Comma separated string-ENUM
email|Limits responses to those associated with specified email address. NOTE: Responses must come from an email collector.|String
first_name|Limits responses to those associated with specified first name. NOTE: Responses must come from an email collector.|String
last_name|Limits responses to those associated with specified last name. NOTE: Responses must come from an email collector.|String
ip|Limits responses to those associated with specified IP address|String
custom|Limits responses to those associated with specified value for [custom field 1](https://help.surveymonkey.com/articles/en_US/kb/Custom-Data). NOTE: Responses must come from an email collector.|String
total_time_max|Limits responses to those that took respondents less time to complete than specified time|String
total_time_min|Limits responses to those that took respondents more time to complete than specified time|String
total_time_units|Determines which unit of time total_time_max and total_time_min use. Accepts: `second`, `minute`, `hour`|String-ENUM


####Rollups Resource

Name | Description | Type
------ | ------- | -------
data[\_].subtype|Question subtype. See [question types](#formatting-question-types) |String-ENUM
data[\_].href|Resource URL for a question's rollup|String
data[\_].id|Question identifier |String
data[\_].family|Question family. See [question types](#formatting-question-types)|String-ENUM
data[\_].summary.answered|Returns the count of respondents who answered the question|Integer
data[\_].summary.skipped|Returns the count of respondents who skipped the question|Integer
data[\_].summary.stats| Returns [basic statistics](https://help.surveymonkey.com/articles/en_US/kb/Basic-Statistics) for close ended questions |Object
data[\_].summary.other_answered|Returns the count of responses who answered the other choice, if available|Integer
data[\_].summary.choices|Returns question's choices with the id and count for each choice|Object


###/surveys/{id}/pages/{id}/rollups

Same as [/surveys/{id}/rollups](#surveys-id-rollups) but returns rollups for only the survey page specified.

###/surveys/{id}/pages/{id}/questions/{id}/rollups

Same as [/surveys/{id}/rollups](#surveys-id-rollups) but returns rollups for only the survey question specified.



###/surveys/{id}/trends

>Definition

```
GET https://api.surveymonkey.net/v3/surveys/{id}/trends
```

>Example Request

```shell
curl -i -X GET -H "Authorization:bearer YOUR_ACCESS_TOKEN" -H "Content-Type": "application/json" https://api.surveymonkey.net/v3/surveys/1234/trends'
```

```python
import requests

s = requests.Session()
s.headers.update({
  "Authorization": "Bearer %s" % YOUR_ACCESS_TOKEN,
  "Content-Type": "application/json"
})

url = "https://api.surveymonkey.net/v3/surveys/%s/trends" % (survey_id)
s.get(url)
```

>Example Response

```json

{
  "per_page": 50,
  "total": 1,
  "data": [
    {
      "subtype": "rating",
      "skipped": 0,
      "href": "https://api.surveymonkey.com/v3/surveys/1234/pages/1234/questions/1234/trends",
      "family": "matrix",
      "answered": 2,
      "trends": [
        {
          "start": "2016-11-01T00:00:00+00:00",
          "rows": [
            {
              "max": 1,
              "total": 2,
              "id": "1234",
              "choices": [
                {
                  "count": 0,
                  "id": "1234"
                },
                {
                  "count": 0,
                  "id": "1234"
                },
                {
                  "count": 1,
                  "id": "1234"
                },
                {
                  "count": 0,
                  "id": "1234"
                },
                {
                  "count": 1,
                  "id": "1234"
                }
              ]
            }
          ],
          "end": "2016-12-01T00:00:00+00:00"
        }
      ],
      "id": "1234",
      "trend_by": "month"
    }
  ],
  "page": 1,
  "links": {
    "self": "https://api.surveymonkey.com/v3/surveys/1234/trends?page=1&per_page=50"
  }
}

```

####Available Methods

 * `HEAD`: Checks if resource is available
 * `OPTIONS`: Returns available methods and options
 * `GET`: Returns answer counts for a particular time periods. Public App users need access to the **View Response Details** [scope](#scopes)

####Optional Query Strings for GET (Accepts same as [/rollups](#rollups) and the following additions)

Name | Description | Data Type
------ | ------- | -------
first_respondent|Limits responses to those completed after the specified respondent id|String
last_respondnet|Limits responses to those completed before the specified respondent id|String
trend_by|Sets the period of time trends are broken into. Accepts: `year`, `quarter`, `month`, `week`, `day`, `hour`|String-ENUM


###/surveys/{id}/pages/{id}/trends

Same as [/surveys/{id}/trends](#surveys-id-trends) but returns trends for only the survey page specified.

###/surveys/{id}/pages/{id}/questions/{id}/trends

Same as [/surveys/{id}/trends](#surveys-id-trends) but returns trends for only the survey question specified.
