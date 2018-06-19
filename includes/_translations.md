##Translations for Multilingual Surveys

These endpoints let you view and create translations for a [multilingual survey](https://help.surveymonkey.com/articles/en_US/kb/Multilingual-Surveys). Use GET [/survey_languages](#survey_languages) to see all available languages and their codes, a GET to [/surveys/{survey_id}/languages/{language_code}](#surveys-survey_id-languages-language_code) to get all strings for translation, and a POST to [/surveys/{survey_id}/languages/{language_code}](#surveys-survey_id-languages-language_code) create a translation.

###/surveys/{survey_id}/languages

>Definition

```
GET https://api.surveymonkey.com/v3/surveys/{survey_id}/languages

```

>Example Request

```shell

curl -i -X GET -H "Authorization: bearer YOUR_ACCESS_TOKEN" -H "content-Type":"application/json" https://api.surveymonkey.com/v3/surveys/{survey_id}/languages

```


```python

import requests

s = request.session()
s.headers.update({
  "Authorization":"Bearer %s" % YOUR_ACCESS_TOKEN,
  "Content-Type":"application/json"
})

url = "https://api.surveymonkey.com/v3/surveys/%s/languages" % (survey_id)
s.get(url)

```

>Example Response

```
{
	"per_page": 50,
	"total": 1,
	"data": [{
				"stale_string_count": 0,
				"translated_string_count": 4,
				"href": "https://api.surveymonkey.com/v3/surveys/1234/languages/fr",
				"inherited_string_count": 0,
				"string_count": 8,
				"name": "French"
				"native_name":"fran\u00e7ais"
				"enabled": true,
				"id": "fr"
			}
		],
	"page": 1,
	"links": {
	"self": "https://api.surveymonkey.com/v3/surveys/1234/languages/?page=1&per_page=50"
	}
}
```

####Available Methods

 * `HEAD`: Checks if resource is available
 * `OPTIONS`: Returns available methods and options
 * `GET`: Returns all existing translations

####Optional Query Strings for GET

Name | Description | Data Type
------ | ------- | -------
page | Which page of resources to return. Defaults to 1 | Integer
per_page | Number of resources to return per page. | Integer


####Translations List Resource

Name | Description | Data Type
------ | ------- | -------
data[\_].stale_string_count|Count of strings that have been updated in the source language since the translation was last updated|Integer
data[\_].translated_string_count|Count strings that have `translations`|Integer
data[\_].href|Resource URL|String
data[\_].inherited_string_count|Count of strings that have empty `translations` but have a parent translation with an existing `translation` they can fall back to|Integer
data[\_].string_count|Count of strings in the survey|Integer
data[\_].name|The name of the language in English|String
data[\_].native_name|The name of the language in the language itself|String
data[\_].enabled|If True, translation is available for respondents to select|Boolean
data[\_].id|Language code for the translation|String

###/surveys/{survey_id}/languages/{language_code}

>Definition

```
POST https://api.surveymonkey.com/v3/surveys/{survey_id}/languages/{language_code}

```

>Example Request

```shell

curl -i -X POST -H "Authorization: bearer YOUR_ACCESS_TOKEN" -H "content-Type":"application/json" https://api.surveymonkey.com/v3/surveys/{survey_id}/languages/fr -d '{"translations":[{"default":"Next","translation":"Suiv.","context":"survey_next","resource_id":"1234"},{"default":"Prev","translation":"Préc.","context":"survey_prev", "resource_id":"1234"},{"default":"Done", "translation":"Terminé", "context":"survey_done", "resource_id":"1234"},{"default":"Exit", "translation":"Quitter", "context":"survey_exit", "resource_id":"1234"
      },{"default":"Thank you for completing our survey!", "translation":"Merci d'avoir répondu à notre sondage!", "context":"collector_disqualification", "resource_id":"1234"}, {"default":"Are you multilingual?", "translation":"Êtes-vous multilingue?", "context":"question_heading", "resource_id":"5678"},{"default":"Yes", "translation":"Oui", "context":"question_option_text", "resource_id":"8912"},{"default":"No", "translation":"Non", "context":"question_option_text", "resource_id":"3456"}, {"default":"My Survey", "translation":"Mon Sondage", "context":"survey_title_html", "resource_id":"1234"}], "enabled":true}

```


```python

import requests

s = request.session()
s.headers.update({
  "Authorization":"Bearer %s" % YOUR_ACCESS_TOKEN,
  "Content-Type":"application/json"
})

payload = {

{
   "href":"https://api.surveymonkey.com/v3/surveys/1234/languages/fr",
   "translations":[
      {
         "default":"Next",
         "translation":"Suiv.",
         "context":"survey_next",
         "resource_id":"1234"
      },
      {
         "default":"Prev",
         "translation":"Préc.",
         "context":"survey_prev",
         "resource_id":"1234"
      },
      {
         "default":"Done",
         "translation":"Terminé",
         "context":"survey_done",
         "resource_id":"1234"
      },
      {
         "default":"Exit",
         "translation":"Quitter",
         "context":"survey_exit",
         "resource_id":"1234"
      },
      {
         "default":"Thank you for completing our survey!",
         "translation":"Merci d'avoir répondu à notre sondage!",
         "context":"collector_disqualification",
         "resource_id":"1234"
      },
      {
         "default":"Are you multilingual?",
         "translation":"Êtes-vous multilingue?",
         "context":"question_heading",
         "resource_id":"5678"
      },
      {
         "default":"Yes",
         "translation":"Oui",
         "context":"question_option_text",
         "resource_id":"8912"
      },
      {
         "default":"No",
         "translation":"Non",
         "context":"question_option_text",
         "resource_id":"3456"
      },
      {
         "default":"My Survey",
         "translation":"Mon Sondage",
         "context":"survey_title_html",
         "resource_id":"1234"
      }
   ],
   "name":"French",
   "native_name":"fran\u00e7ais",
   "enabled":true,
   "id":"fr"
}


url = "https://api.surveymonkey.com/v3/surveys/%s/languages/fr" % (survey_id)
s.get(url, json=payload)

```

>Example Response for GET. POST and PATCH return an empty body

```

{
   "href":"https://api.surveymonkey.com/v3/surveys/1234/languages/fr",
   "translations":[
      {
         "default":"Next",
         "translation":"Suiv.",
         "context":"survey_next",
         "resource_id":"1234"
      },
      {
         "default":"Prev",
         "translation":"Préc.",
         "context":"survey_prev",
         "resource_id":"1234"
      },
      {
         "default":"Done",
         "translation":"Terminé",
         "context":"survey_done",
         "resource_id":"1234"
      },
      {
         "default":"Exit",
         "translation":"Quitter",
         "context":"survey_exit",
         "resource_id":"1234"
      },
      {
         "default":"Thank you for completing our survey!",
         "translation":"Merci d'avoir répondu à notre sondage!",
         "context":"collector_disqualification",
         "resource_id":"1234"
      },
      {
         "default":"Are you multilingual?",
         "translation":"",
         "context":"question_heading",
         "resource_id":"5678"
      },
      {
         "default":"Yes",
         "translation":"Oui",
         "context":"question_option_text",
         "resource_id":"8912"
      },
      {
         "default":"No",
         "translation":"Non",
         "context":"question_option_text",
         "resource_id":"3456"
      },
      {
         "default":"My Survey",
         "translation":"Mon Sondage",
         "context":"survey_title_html",
         "resource_id":"1234"
      }
   ],
   "enabled":true,
   "id":"fr"
}


```


####Available Methods

 * `HEAD`: Checks if resource is available
 * `OPTIONS`: Returns available methods and options
 * `GET`: Returns existing translations or the translation structure
 * `POST`: Creates a translation
 * `PATCH`: Updates a translation
 * `DELETE`: Deletes a translation

####Request Body Arguments for POST and PATCH

Name | Required |Description | Data Type
----- | ------ |------ | -----
enabled| No | If True, translation is available for respondents to select | Boolean|
translations | Yes | List of translation objects. Each object represents a string in the survey. At least one is required for POST and PATCH. See below for structure.| Array|

####Translation Object

Name |Description | Data Type
----- | ------ |------ | -----
default| The text from the default language for the survey.|String
translation|Translated text shown when a respondent chooses the survey in this language. Translate a survey by filling in all empty translations,|String
context|Describes the string's role in the survey|String
id|Survey, question or answer option id related to the string|String


