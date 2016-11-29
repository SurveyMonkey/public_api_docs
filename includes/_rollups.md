##Response Counts and Trends

The following endpoints let you view how many respondents answered a question a particular way and trends in how many respondents answered a question a particular way in a given time period, for example a week.

<aside class="notice"><strong>NOTE for Public Apps</strong>: The View Response Details scope requires a SurveyMonkey annual<a href="https://www.surveymonkey.com/pricing/?ut_source=dev_portal&amp;ut_source2=docs">paid plan</a>.</aside>

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
 * `GET`: Returns rollups for all questions in a survey. Requires **View Response Details** [scope](#scopes)

####Optional Query Strings for GET

Name | Description | Type
------ | ------- | -------
collector_ids|Limits to responses from specified collectors|Comma separated collector ids
start_created_at|Limits to responses created after date specified|Date String
end_created_at|Limits to responses created before date specified|Date String
start_modified_at|Limits to responses last modified after date specified|Date String
end_modified_at|Limits to responses last modified before date specified|Date String
status|Limits responses to those of a certain status. Accepts: 'completed', 'partial', 'overquota', 'disqualified'|Comma separated strings 
email|Limits responses to those associated with an email address. NOTE: Responses must come from an email collector.|String
first_name|Limits responses to those associate with specified first name. NOTE: Responses must come from an email collector.|String
last_name|Limits responses to those associate with specified last name. NOTE: Responses must come from an email collector.|String
ip||IP
custom|Limits responses to those associate with specified value for [custom field 1](https://help.surveymonkey.com/articles/en_US/kb/Custom-Data). NOTE: Responses must come from an email collector.|String
total_time_max|Limits responses to those that took respondents less time to complete than specified time|String
total_time_min|Limits responses to those that took respondents more time to complete than specified time|String
total_time_units|Determines which unit of time total_time_max and total_time_min use. Accepts: 'second', 'minute', 'hour'|String


####Rollups Resource

Name | Description | Type
------ | ------- | -------
data[\_].subtype|Question subtype. See [question types](#formatting-question-types) |String
data[\_].href|Resource URL for a question's rollup|String
data[\_].id|Question id |String
data[\_].family|Question family. See [question types](#formatting-question-types)|String
data[\_].summary.answered|Returns the count of respondents who answered the question|Integer
data[\_].summary.skipped|Returns the count of respondents who skipped the question|Integer
data[\_].summary.stats| Returns [basic statistics](https://help.surveymonkey.com/articles/en_US/kb/Basic-Statistics) for close ended questions |Object
data[\_].summary.other_answered||
data[\_].summary.choices|Returns question's choices with the id and count for each choice|Object|


###/surveys/{id}/pages/{id}/rollups

Same as [/surveys/{id}/rollups](#surveys-id-rollups) but returns rollups for only the survey page specified. 

###/surveys/{id}/pages/{id}/questions/{id}/rollups

Same as [/surveys/{id}/rollups](#surveys-id-rollups) but returns rollups for only the survey question specified. 


<aside class="notice">Trends are not available for file_upload, slider, presentation, demographic, matrix_menu, or datetime question types and trends object will return empty for these questions.</aside>

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
 * `GET`: Returns answer counts for a particular time period. Requires **View Response Details** [scope](#scopes)

####Optional Query Strings for GET (Accepts same as [/rollups](#rollups) and the following additions)

Name | Description | Type
------ | ------- | -------
first_respondent|Limits to responses completed after the specified respondent|Respondent id
last_respondnet|Limits to responses completed before the specified respondent|Respondent id
trend_by|Sets the period of time trends are broken into. Accepts: 'year', 'quarter', 'month', 'week', 'day', 'hour'|String


####Trends Resource

Name | Description | Type
------ | ------- | -------

###/surveys/{id}/pages/{id}/trends

Same as [/surveys/{id}/trends](#surveys-id-trends) but returns trends for only the survey page specified. 

###/surveys/{id}/pages/{id}/questions/{id}/trends

Same as [/surveys/{id}/trends](#surveys-id-trends) but returns trends for only the survey question specified. 
