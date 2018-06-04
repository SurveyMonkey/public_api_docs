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

####Questions List Resource

Name | Description | Data Type
------ | ------- | -------
data[\_].text | The text in the question | String
data[\_].modifiers | Modifiers that the question allows. e.g. ("this company", "this brand, "this product") (empty for Custom QB)| Array
data[\_].locales | A list of locales that the question supports (empty for Custom QB) | Array of Strings
data[\_].question_id | id of the question, to be used in creating it | String
