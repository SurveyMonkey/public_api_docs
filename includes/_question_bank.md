##Question Bank

The following endpoint lets you get a list of questions that exist in the question bank.  You can then use these to create a question in a survey (See [formatting question types](#formatting-question-types)).


###/question_bank/questions

>Definition

```
GET https://api.surveymonkey.com/v3/question_bank/questions
```


>Example Request

```shell
curl -i -X GET -H "Authorization:bearer YOUR_ACCESS_TOKEN" -H "Content-Type": "application/json" https://api.surveymonkey.com/v3/question_bank/questions
```

```python
import requests

s = requests.Session()
s.headers.update({
  "Authorization": "Bearer %s" % YOUR_ACCESS_TOKEN,
  "Content-Type": "application/json"
})

url = "https://api.surveymonkey.com/v3/question_bank/questions"
s.get(url)
```
>Example Response

```json
{
    "per_page": 50,
    "total": 2675,
    "data": [
        {
            "text": "How likely is it that you would recommend () to a friend or colleague?",
            "modifiers": [
                {
                    "modifier_type": "open_ended",
                    "options": [
                        {
                            "value": "this company",
                            "modifier_options_id": "36237"
                        },
                        {
                            "value": "this brand",
                            "modifier_options_id": "36238"
                        },
                        {
                            "value": "this product",
                            "modifier_options_id": "36627"
                        },
                        {
                            "value": "this service",
                            "modifier_options_id": "36628"
                        },
                        {
                            "value": "Specify company, brand, product or service",
                            "modifier_options_id": "36629"
                        }
                    ],
                    "modifier_id": "13848"
                }
            ],
            "locales": [
                "en_AU",
                "en_CA",
                "en_GB",
                "en_US"
            ],
            "question_id": "669"
        }
    ]
}
```


####Available Methods

 * `HEAD`: Checks if resource is available
 * `OPTIONS`: Returns available methods and options
 * `GET`: Returns a list of question bank questinos available to the user

####Optional Query Strings for GET

Name | Description | Data Type
------ | ------- | -------
page | Which page of resources to return. Defaults to 1 | Integer
per_page | Number of resources to return per page | Integer
locale | Return questions for this locale, (see `/v3/survey_languages`), defaults to `en_US` | String-ENUM
search | Return only questions containing (or related to) this text | String
custom | Whether to look through the regular Question Bank, or a Team's Custom Question Bank, defaults to `false` | Boolean

####Survey List Resource

Name | Description | Data Type
------ | ------- | -------
data[\_].text | The text in the question | String
data[\_].modifiers | Modifiers that the question allows. e.g. ("this company", "this brand, "this product") (empty for Custom QB)| Array
data[\_].locales | A list of locales that the question supports (empty for Custom QB) | Array of Strings
data[\_].question_id | id of the question, to be used in creating it | Integer




>Definition

```
POST https://api.surveymonkey.com/v3/surveys/{survey_id}/pages/{page_id}/questions
```


>Example Request

```shell
curl -i -X POST -H "Authorization:bearer YOUR_ACCESS_TOKEN" -H "Content-Type": "application/json" https://api.surveymonkey.com/v3/surveys/{survey_id}/pages/{page_id}/questions -d '{"question_bank": {"question_bank_question_id": "669","modifier_options": {"36628": null}}}'


```

```python
import requests

s = requests.Session()
s.headers.update({
  "Authorization": "Bearer %s" % YOUR_ACCESS_TOKEN,
  "Content-Type": "application/json"
})
payload = 
url = "https://api.surveymonkey.com/v3/surveys/{survey_id}/pages/{page_id}/questions"
s.post(url, json=payload)
```
>Example Response

```json
{
    "sorting": null,
    "family": "matrix",
    "subtype": "rating",
    "required": null,
    "answers": {
        "rows": [
            {
                "visible": true,
                "text": "",
                "position": 1,
                "id": "3163619866"
            }
        ],
        "choices": [
            {
                "description": "Not at all likely",
                "weight": -100,
                "visible": true,
                "id": "3163619867",
                "is_na": false,
                "text": "Not at all likely - 0",
                "position": 1
            },
            {
                "description": "",
                "weight": -100,
                "visible": true,
                "id": "3163619868",
                "is_na": false,
                "text": "1",
                "position": 2
            },
            {
                "description": "",
                "weight": -100,
                "visible": true,
                "id": "3163619869",
                "is_na": false,
                "text": "2",
                "position": 3
            },
            {
                "description": "",
                "weight": -100,
                "visible": true,
                "id": "3163619870",
                "is_na": false,
                "text": "3",
                "position": 4
            },
            {
                "description": "",
                "weight": -100,
                "visible": true,
                "id": "3163619871",
                "is_na": false,
                "text": "4",
                "position": 5
            },
            {
                "description": "",
                "weight": -100,
                "visible": true,
                "id": "3163619872",
                "is_na": false,
                "text": "5",
                "position": 6
            },
            {
                "description": "",
                "weight": -100,
                "visible": true,
                "id": "3163619873",
                "is_na": false,
                "text": "6",
                "position": 7
            },
            {
                "description": "",
                "weight": 0,
                "visible": true,
                "id": "3163619874",
                "is_na": false,
                "text": "7",
                "position": 8
            },
            {
                "description": "",
                "weight": 0,
                "visible": true,
                "id": "3163619875",
                "is_na": false,
                "text": "8",
                "position": 9
            },
            {
                "description": "",
                "weight": 100,
                "visible": true,
                "id": "3163619876",
                "is_na": false,
                "text": "9",
                "position": 10
            },
            {
                "description": "Extremely likely",
                "weight": 100,
                "visible": true,
                "id": "3163619877",
                "is_na": false,
                "text": "Extremely likely - 10",
                "position": 11
            }
        ]
    },
    "visible": true,
    "href": "https://api.localmonkey.com/v3/surveys/111380075/pages/116044697/questions/338792202",
    "headings": [
        {
            "heading": "How likely is it that you would recommend this service to a friend or colleague?"
        }
    ],
    "position": 4,
    "validation": null,
    "id": "338792202",
    "forced_ranking": false
}
```