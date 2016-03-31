##Benchmarks

Benchmark data comes from SurveyMonkey customers who used [Question Bank](http://help.surveymonkey.com/articles/en_US/kb/What-is-Question-Bank) questions in their surveys. Organizations of all shapes and sizes use Question Bank, like local coffee shops, schools, and Fortune 500 companies. Benchmarks give context to your survey results by allowing you to compare your results to others who used the same Question Bank questions as you.

<aside class="notice">
<a href="http://help.surveymonkey.com/articles/en_US/kb/Benchmarks">Benchmarks</a> are available as an add on only. If you are interested in benchmarks please contact: <a href="mailto: benchmarksales@surveymonkey.com">benchmarksales@surveymonkey.com</a>.</aside>

###/benchmark_bundles

>Definition

```
GET https://api.surveymonkey.net/v3/benchmark_bundles
```

>Example Request

```shell
curl -i -X GET -H "Authorization:bearer YOUR_ACCESS_TOKEN" https://api.surveymonkey.net/v3/benchmark_bundles?api_key=YOUR_API_KEY
```

```python
import requests

s = requests.session()

url = "https://api.surveymonkey.net/v3/benchmark_bundles?api_key=%s" % YOUR_API_KEY
s.get(url)
```

>Example Response

```json
{
  "per_page": 5,
  "data": [
    {
      "href": "https://api.surveymonkey.net/v3/benchmark_bundles/nps_education",
      "id": "nps_education",
      "title": "All Education"
    },
    {
      "href": "https://api.surveymonkey.net/v3/benchmark_bundles/nps_higher_education",
      "id": "nps_higher_education",
      "title": "Higher Education"
    },
    {
      "href": "https://api.surveymonkey.net/v3/benchmark_bundles/nps_schools",
      "id": "nps_schools",
      "title": "K-12 Schools"
    },
    {
      "href": "https://api.surveymonkey.net/v3/benchmark_bundles/nps_sports_instruction",
      "id": "nps_sports_instruction",
      "title": "Sports Instruction"
    },
    {
      "href": "https://api.surveymonkey.net/v3/benchmark_bundles/nps_health_human_services",
      "id": "nps_health_human_services",
      "title": "Health and Human Services"
    }
  ],
  "page": 1
}
```

####Available Methods

 * `HEAD`: Checks if resource is available
 * `OPTIONS`: Returns available methods
 * `GET`: Returns a list of benchmark bundles you have access to

####Optional Query Strings for GET

Name | Description | Type
------ | ------- | -------
page | Page of resources to return. Defaults to 1 | Integer
per_page | Number of resources to return per page | Integer
country | Country to get the bundles for. Defaults to US | String

####Bundle List

Name | Description | Type
------ | ------- | -------
data.id | Benchmark Bundle id | String
data.title | Benchmark Bundle name | String
data.href |  Benchmark Bundle resource link| String

###/benchmark_bundles/{id}

>Definition

```
GET https://api.surveymonkey.net/v3/benchmark_bundles/{bundle_id}
```

>Example Request

```shell
curl -i -X GET -H "Authorization:bearer YOUR_ACCESS_TOKEN" https://api.surveymonkey.net/v3/benchmark_bundles/test_bundle?api_key=YOUR_API_KEY
```

```python
import requests

s = requests.session()

url = "https://api.surveymonkey.net/v3/benchmark_bundles/%s?api_key=%s" % (bundle_id, YOUR_API_KEY)
s.get(url)
```

>Example Response

```json
{
  "title": "Consumer Goods and Services",
  "details": {
    "bullets": [
      "Includes retail companies, restaurants, and other consumer based industries",
      "2,600 responses per question (average)"
    ],
    "subtext": "Responses from 40+ organizations*"
  },
  "questions": [
    {
      "answer_order": "normal",
      "id": "25651",
      "answers": {
        "choices": [
          {
            "text": "Strongly Disagree"
          },
          {
            "text": "Disagree"
          },
          {
            "text": "Neutral/Neither agree nor disagree"
          },
          {
            "text": "Agree"
          },
          {
            "text": "Strongly Agree"
          }
        ]
      },
      "title": "My organization is dedicated to diversity and inclusiveness."
    },
  ],
  "id": "test_bundle"
}
```

####Available Methods

 * `HEAD`: Checks if resource is available
 * `OPTIONS`: Returns available methods and options
 * `GET`: Returns the questions and details included in a given bundle

####Bundle Details

Name | Description | Type
------ | ------- | -------
id | Benchmark Bundle id | String
title | Benchmark Bundle name | String
details | Benchmark Bundle description | String
questions | The questions associated with the bundle | List


###/benchmark_bundles/{id}/analyze

>Definition

```
GET https://api.surveymonkey.net/v3/benchmark_bundles/{bundle_id}/analyze
```

>Example Request

```shell
curl -i -X GET -H "Authorization:bearer YOUR_ACCESS_TOKEN" 'https://api.surveymonkey.net/v3/benchmark_bundles/test_bundle/analyze?api_key=YOUR_API_KEY&question_ids=25651,25652'

```

```python
import requests

s = requests.session()

payload = {
  'question_ids': [123, 456],
  'percentile_start': 1,
  'percentile_end': 100
}
url = "https://api.surveymonkey.net/v3/benchmark_bundles/%s/analyze?api_key=%s" % (bundle_id, YOUR_API_KEY)
s.get(url, params=payload)
```

>Example Response

```json
{
  "date_end": "2015-12-31T00:00:00+00:00",
  "date_start": "2015-01-01T00:00:00+00:00",
  "id": "test_bundle",
  "benchmarks": [
    {
      "num_data_points": 50,
      "distribution_values": {
        "1": 0.0333333333,
        "3": 0.2222222222,
        "2": 0.0555555555,
        "5": 0.2222222222,
        "4": 0.4444444444
      },
      "question": {
        "answer_order": "normal",
        "id": "25651",
        "answers": {
          "choices": [
            {
              "text": "Strongly Disagree"
            },
            {
              "text": "Disagree"
            },
            {
              "text": "Neutral/Neither agree nor disagree"
            },
            {
              "text": "Agree"
            },
            {
              "text": "Strongly Agree"
            }
          ]
        },
        "title": "My organization is dedicated to diversity and inclusiveness."
      },
      "num_responses": 1000,
      "quartile_values": {
        "100": 5.4343,
        "0": 1.9,
        "75": 2.011,
        "50": 5.211,
        "25": 8.2
      }
    }
  ]
}

```
####Available Methods

 * `HEAD`: Checks if resource is available
 * `OPTIONS`: Returns available methods and options
 * `GET`: Returns the benchmark for the given bundle

####Query String for GET

Name | Description | Type
------ | ------- | -------
question_ids (required) | List of question to recieve analytics for. | Comma Separated List
percentile_start (optional)  | Starting percentile to filter by (default=0). | Integer
percentile_end (optional) | Ending percentile to filter by (default=100). | Integer

####Bundle Benchmark

Name | Description | Type
------ | ------- | -------
id  | Benchmark Bundle id | String
date_start | Start date for included responses in the benchmark | String
date_end  | End date for included responses in the benchmark | String
benchmarks | List of benchmark results for each question in the bundle, with the question details | List


