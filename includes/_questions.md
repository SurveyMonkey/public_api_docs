###/surveys/{id}/pages/{id}/questions

>Definition

```
POST https://api.surveymonkey.net/v3/surveys/{survey_id}/pages/{page_id}/questions
```

>Example Request

```shell
curl -i -X POST -H "Authorization:bearer YOUR_ACCESS_TOKEN" -H "Content-Type": "application/json" https://api.surveymonkey.net/v3/surveys/{survey_id}/pages/{page_id}/questions -d '{"headings": [{"heading": "A question about primates.", "random_assignment": {"percent": 50, "position": 1}},{"heading": "A question about primates phrased slightly differently.", "random_assignment": {"percent": 50, "position": 2},}], "family": "open_ended", "subtype": "single", "position": 1, "sorting": {"type": "textasc","ignore_last": True}, "required": {"text": "This question is required!", "type": "at_least", "amount": "1"},"validation": {"type": "integer","text": "Validation has failed!","min": 20,"max": 30}, "forced_ranking": True, "answers": { #SEE ANSWERS SECTION }}'

```


```python
import requests

s = requests.session()
s.headers.update({
  "Authorization": "Bearer %s" % YOUR_ACCESS_TOKEN,
  "Content-Type": "application/json"
})

payload = {
  "headings": [
    {
      "random_assignment": {
        "position": 1,
        "percent": 50
      },
      "heading": "Multiple Choice with Random Assignment v1"
    },
    {
      "random_assignment": {
        "position": 2,
        "percent": 50
      },
      "heading": "Multiple Choice with Random Assignment v2"
    }
  ],
  "family": "single_choice",
  "subtype": "vertical",
  "answers": {
    "choices": [
      {
        "text": "a",
        "visible": true,
        "position": 1
      },
      {
        "text": "b",
        "visible": true,
        "position": 2
      },
      {
        "text": "c",
        "visible": true,
        "position": 3
      }
    ]
  },
  "position": 3
}
url = "https://api.surveymonkey.net/v3/surveys/%s/pages/%s/questions" % (survey_id, page_id)
s.post(url, json=payload)

####Response
Same as request, but with two additional fields (id, href)

```

####Available Methods

 * `HEAD`: Checks if resource is available
 * `OPTIONS`: Returns available methods and options
 * `GET`: Returns a list of questions on a survey page. Public App users need access to the **View Surveys** [scope](#scopes)
 * `POST`: Creates a new question on a survey page, see [formatting question types](#formatting-question-types). Public App users need access to the **Create/Modify Surveys** [scope](#scopes)

####Optional Query Strings for GET

Name | Description | Data Type
------ | ------- | -------
page | Which page of resources to return. Defaults to 1 | Integer
per_page | Number of resources to return per page | Integer

####Question List Resource

Name | Description | Data Type
------ | ------- | -------
data[\_].id | Question id | String
data[\_].heading | Question heading | String
data[\_].href | Resource API URL | String
data[\_].position | Position of question on page | Integer

####Request Body Arguments for POST

Name | Required |Description | Data Type
----- | ------ |------ | -----
headings | Yes |List of question headings objects | Array
headings[\_].heading | Yes |The title of the question, or empty string if `random_assignment` is defined | String
headings[\_].description | No | If `random_assignment` is defined, and `family` is `presentation_image` this is the title | String
headings[\_].image | No |Image data when question `family` is `presentation_image`| Object or null
headings[\_].image.url | No | URL of image when question `family` is `presentation_image`| String
headings[\_].random_assignment | No |Random assignment data | Object or null
headings[\_].random_assignment.percent | Yes |Percent chance of this random assignment showing up (must sum to 100) | Integer
headings[\_].random_assignment.position | No |Position of the random_assignment in survey creation page | Integer
headings[\_].random\_assignment.variable\_name | No |Internal use name for question tracking, can be `""` | String
position | No (default=last) | Position of question on page | Integer
family | Yes | Question family determines the type of question, see [formatting question types](#formatting-question-types) | String
subtype | Yes | Question family's subtype further specifies the type of question, see [formatting question types](#formatting-question-types)  | String
sorting | No | Sorting details of answers | Object
sorting.type | Yes | Sort answer choices by: `default`, `textasc`, `textdesc`, `resp_count_asc`, `resp_count_desc`, `random`, `flip`| String-ENUM
sorting.ignore_last| No | If true, does not sort the last answer option (useful for "none of the above", etc) | Boolean
required | No | Whether an answer is required for this question | Object
required.text | Yes | Text to display if a required question is not answered | String
required.type | Yes if question is matrix_single, matrix_ranking, and matrix menu | Specifies how much of the question must be answered: `all` , `at_least`, `at_most`, `exactly`, or `range` | String-ENUM
required.amount | Yes if type is defined | The amount of answers required to be answered. If the required type is range then this is two numbers separated by a comma, as a string (e.g. "1,3" to represent the range of 1 to 3). | String
validation | No | Whether the answer must pass certain validation parameters | Object
validation.type | Yes | Type of validation to use: `any`, `integer`, `decimal`, `date_us`, `date_intl`, `regex`, `email`, or `text_length` | String-ENUM
validation.text | Yes | Text to display if validation fails | String
validation.min | Yes | Minimum value an answer can be to pass validation | Date string, integer, or null depending on validation.type
validation.max | Yes| Maximum value an answer can be to pass validation | Date string, integer, or null depending on validation.type
validation.sum | No | Only accepted is family=open_ended and subtype=numerical, the exact integer textboxes must sum to in order to pass validation | Integer
validation.sum_text | No | Only accepted is family=open_ended and subtype=numerical, the message to display if textboxes do not sum to validation.sum | String
forced_ranking | No | Required if type is matrix and subtype is rating or single, whether or not to force ranking | Boolean
answers |Yes for all question types except open_ended_single| Answers object, refer to [Formatting Question Types](#formatting-question-types) | Object
display_options | Yes for File Upload, Slider, & Emoji/Star Rating [question types](#formatting-question-types)| Display option object, refer to [Formatting Question Types](#formatting-question-types) | Object

####Response Resource

Name  |Description | Type
----- |------ | -----
headings  |Question heading | Array
headings[\_].heading  |The title of the question, or empty string if `random_assignment` is defined | String
headings[\_].description  | If `random_assignment` is defined, and `family` is `presentation_image` this is the title | String
headings[\_].image  |Image data when question `family` is `presentation_image`| Object or null
headings[\_].image.url  | URL of image when question `family` is `presentation_image`| String
headings[\_].random_assignment  |Random assignment data | Object or null
headings[\_].random_assignment.percent  |Percent chance of this random assignment showing up (must sum to 100) | Integer
headings[\_].random_assignment.position  |Position of the random_assignment in survey creation page | Integer
headings[\_].random\_assignment.variable\_name  |Internal use name for question tracking, can be `""` | String
headings[\_].random\_assignment.id  |Internal use id for question tracking | String
position  | Position of question on page | Integer
visible  | Whether the question is visible (corresponds with being deleted in the UI) | Boolean
family  | Question family, see [formatting question types](#formatting-question-types) | String
subtype  | Question family's subtype, see [formatting question types](#formatting-question-types)  | String
sorting  | Sorting details of answers | Object
sorting.type  | Sort answer choices by: `default`, `textasc`, `textdesc`, `resp_count_asc`, `resp_count_desc`, `random`, `flip`| String-ENUM
sorting.ignore_last | If true, does not sort the last answer option (useful for "none of the above", etc) | Boolean
required  | Whether an answer is required for this question | Object
required.text  | String to display if a required question is not answered | String
required.type  | Required type for matrix questions: `all` , `at_least`, `at_most`, `exactly`, or `range` | String-ENUM
required.amount  | The amount of answers required to be answered. If the required type is range then this is two numbers separated by a comma, as a string (e.g. "1,3" to represent the range of 1 to 3). | String
validation  | Whether the answer must pass certain validation parameters | Object
validation.type  | Type of validation to use: `any`, `integer`, `decimal`, `date_us`, `date_intl`, `regex`, `email`, or `text_length` | String-ENUM
validation.text  | Text to display if validation fails | String
validation.min  | Minimum value an answer can be to pass validation | Date string, integer, or null depending on validation.type
validation.max | Maximum value an answer can be to pass validation | Date string, integer, or null depending on validation.type
validation.sum  | Only accepted is family=open_ended and subtype=numerical, the exact integer textboxes must sum to in order to pass validation | Integer
validation.sum_text  | Only accepted is family=open_ended and subtype=numerical, the message to display if textboxes do not sum to validation.sum | String
forced_ranking  | If type is matrix and subtype is rating or single, whether or not to force ranking | Boolean
answers | Answers object, refer to [Formatting Question Types](#formatting-question-types) | Object
id | Question id | String

###/surveys/{id}/pages/{id}/questions/{id}

>Definition

```
GET https://api.surveymonkey.net/v3/surveys/{survey_id}/pages/{page_id}/questions/{question_id}
```

>Example Request

```shell
curl -i -X POST -H "Authorization:bearer YOUR_ACCESS_TOKEN" -H "Content-Type": "application/json" https://api.surveymonkey.net/v3/surveys/{survey_id}/pages/{page_id}/questions/{question_id}

```

```python
import requests

s = requests.session()
s.headers.update({
  "Authorization": "Bearer %s" % YOUR_ACCESS_TOKEN,
  "Content-Type": "application/json"
})

url = "https://api.surveymonkey.net/v3/surveys/%s/pages/%s/questions/%s" % (survey_id, page_id, question_id)
s.get(url)

####Response

Same as `POST` [/surveys/{id}/pages/questions](#surveys-id-pages-id-questions)

```

####Available Methods

 * `HEAD`: Checks if resource is available
 * `OPTIONS`: Returns available methods and options
 * `GET`: Returns a question. Requires **View Surveys** [scope](#scopes)
 * `PATCH`: Updates a question (updates any fields accepted as arguments to `POST` [/surveys/{id}/pages/questions](#surveys-id-pages-id-questions). Public App users need access to the **Create/Modify Surveys** [scope](#scopes)
 * `PUT`: Replaces a question (same arguments and requirements as `POST` [/surveys/{id}/pages/questions](#surveys-id-pages-id-questions). Public App users need access to the **Create/Modify Surveys** [scope](#scopes)
 * `DELETE`: Deletes a question. Public App users need access to the **Create/Modify Surveys** [scope](#scopes)

###Formatting Question Types

All questions have a`family` and `subtype` that define their type and some questions have a `display_type` and `display_subtype` that further define their type. See below for example formatting of the answers object  and display_options object for different question types. Read more about SurveyMonkey's question types in our [help center](http://help.surveymonkey.com/articles/en_US/kb/Available-question-types-and-formatting-options).

|Family|Subtype|Display_Type|Display_Subtype
|------|-------|--------------|------------|
|single_choice|'vertical', 'horiz', 'menu'|NA|NA|
|matrix| 'single', 'rating', 'ranking', 'menu', 'multi'|'emoji' (with 'ranking')|'star'|
|open_ended|'single','multi', 'numerical', 'essay'|'slider', 'file_upload' (with 'single')|NA|
|demographic|'international', 'us'|NA|NA|
|datetime|'both', 'date_only', 'time_only'|NA|NA|
|multiple_choice|'vertical'|NA|NA|
|presentation|'descriptive_text', 'image'|NA|NA|

####Single Choice

>Single Choice

```json
{
    "headings": [
        {
            "heading": "Which monkey would you rather have as a pet?"
        }
    ],
    "position": 1,
    "family": "single_choice",
    "subtype": "vertical",
    "answers": {
        "choices":[
            {
                "text": "Capuchin"
            },
            {
                "text": "Mandrill"
            },
        ],
        "other":[
                {
                    "text": "Other",
                    "num_chars": 100,
                    "num_lines": 3
                }
        ]
    }
}
```
![Single Choice](https://raw.githubusercontent.com/SurveyMonkey/public_api_docs/master/images/single-choice.png)

Name | Description | Data Type
----- | ------ | -----
choices (required) | List of available choices for the user | Array
choices[\_].text (required) | Choice for user selection | String
choices[\_].position (optional) | Position of the current choice | Integer
other (optional) | List of other answer options | Array
other[\_].text | Text to display next to other option | String
other[\_].num_chars | Set a character limit to the option | Integer
other[\_].num_lines | Set a line limit to the option | Integer

####Multiple Choice

>Multiple Choice

```json
{
    "headings": [
        {
            "heading": "Which monkeys would you like as pets?"
        }
    ],
    "position": 1,
    "family": "multiple_choice",
    "subtype": "vertical",
    "answers": {
        "choices":[
            {
                "text": "Capuchin"
            },
            {
                "text": "Mandrill"
            }
        ]
    }
}
```
![Multiple Choice](https://raw.githubusercontent.com/SurveyMonkey/public_api_docs/master/images/multiple-choice.png)

Name | Description | Data Type
----- | ------ | -----
choices (required) | List of available choices for the user | Array
choices[\_].text (required) | Choice for user selection | String
choices[\_].position (optional) | Position of the current choice | Integer
other (optional) | List of other answer options | Array
other[\_].text | Text to display next to other option | String
other[\_].num_chars | Set a character limit to the option | Integer
other[\_].num_lines | Set a line limit to the option | Integer

####Matrix - Single

>Matrix - Single

```json
{
    "headings": [
        {
            "heading": "What is each of your family members' favorite ice cream?"
        }
    ],
    "position": 1,
    "family": "matrix",
    "subtype": "single",
    "forced_ranking": false,
    "answers": {
        "rows": [
            {
                "text": "Mother"
            },
            {
                "text": "Father"
            }
        ],
        "choices": [
            {
                "text": "Chocolate"
            },
            {
                "text": "Vanilla"
            },
            {
                "text": "Strawberry"
            }
        ]
    }
}
```
![Matrix Single](https://raw.githubusercontent.com/SurveyMonkey/public_api_docs/master/images/matrix-single.png)

Name | Description | Data Type
----- | ------ | -----
rows (required) | List of rows in the matrix | Array
rows[\_].text (required) | Text label for the row | String
rows[\_].position (optional) | Position of the row | Integer
choices (required) | List of available choices for the user | Array
choices[\_].text (required) | Choice for user selection | String
choices[\_].position (optional) | Position of the current choice | Integer
other (optional) | List of other answer options | Array
other[\_].text | Text to display next to other option | String
other[\_].num_chars | Set a character limit to the option | Integer
other[\_].num_lines | Set a line limit to the option | Integer

####Matrix - Rating

>Matrix - Rating

```json
{
    "headings": [
        {
            "heading": "What is each of your family members' favorite ice cream?"
        }
    ],
    "position": 1,
    "family": "matrix",
    "subtype": "rating",
    "forced_ranking": false,
    "answers": {
        "rows": [
            {
                "text": "Mother"
            },
            {
                "text": "Father"
            }
        ],
        "choices": [
            {
                "text": "Chocolate",
                "weight": 1
            },
            {
                "text": "Vanilla",
                "weight": 1
            },
            {
                "text": "Strawberry",
                "weight": 1
            }
        ]
    }
}
```
![Matrix Rating](https://raw.githubusercontent.com/SurveyMonkey/public_api_docs/master/images/matrix-rating.png)

Name | Description | Data Type
----- | ------ | -----
rows (required) | List of rows in the matrix | Array
rows[\_].text (required) | Text label for the row | String
rows[\_].position (optional) | Position of the row | Integer
choices (required) | List of available choices for the user | List
choices[\_].text (required) | Choice for user selection | String
choices[\_].weight (required) | Weight value of the choice | Integer
choices[\_].position (optional) | Position of the row | Integer
other (optional) | List of other answer options | Array
other[\_].text | Text to display next to other option | String
other[\_].num_chars | Set a character limit to the option | Integer
other[\_].num_lines | Set a line limit to the option | Integer

####Matrix - Ranking

>Matrix - Ranking

```json
{
    "headings": [
        {
            "heading": "Rank these flavors in terms of your preference!"
        }
    ],
    "position": 1,
    "family": "matrix",
    "subtype": "ranking",
    "answers": {
        "rows":[
            {
                "text": "Vanilla"
            },
            {
                "text": "Chocolate"
            },
            {
                "text": "Strawberry"
            }
        ]
    }
}
```
![Matrix Ranking](https://raw.githubusercontent.com/SurveyMonkey/public_api_docs/master/images/matrix-ranking.png)

Name | Description | Data Type
----- | ------ | -----
rows (required) | List of rows in the matrix | Array
rows[\_].text (required) | Text label for the row | String
rows[\_].position (optional) | Position of the row | Integer

####Matrix - Menu

>Matrix - Menu

```json
{
    "headings": [
        {
            "heading": "Which texture and taste do you prefer on your ice cream?"
        }
    ],
    "position": 1,
    "family": "matrix",
    "subtype": "menu",
    "answers": {
        "rows":[
            {
            "text": "Chocolate"
            },
            {
            "text": "Cookies and Cream"
            }
        ],
        "cols":[
            {
                "text": "Texture",
                "choices": [
                    {
                        "text": "Smooth",
                        "visible": true,
                        "position": 1
                    },
                    {
                        "text": "Chunky",
                        "visible": true,
                        "position": 2
                    }
                ]
            },
            {
                "text": "Flavor",
                "choices": [
                    {
                        "text": "Light",
                        "visible": true,
                        "position": 1
                    },
                    {
                        "text": "Full",
                        "visible": true,
                        "position": 2
                    }
                ]
            }
        ]
    }
}
```
![Matrix Menu](https://raw.githubusercontent.com/SurveyMonkey/public_api_docs/master/images/matrix-menu.png)

Name | Description | Data Type
----- | ------ | -----
rows (required) | List of rows in the matrix | Array
rows[\_].text (required) | Text label for the row | String
rows[\_].position (optional) | Position of the row | Integer
cols (required) | List of columns in the matrix | Array
cols[\_].text (required) | Text label for column | String
cols[\_].choices (required) | List of available choices for the user in dropdown menu | Array
cols[\_].choices[\_].text (required) | Choice for user selection | String
cols[\_].choices[\_].position (required) | Position of choice | Integer
other (optional) | List of other answer options | Array
other[\_].text | Text to display next to other option | String
other[\_].num_chars | Set a character limit to the option | Integer
other[\_].num_lines | Set a line limit to the option | Integer




####Open Ended - Single or Essay

>Open Ended - Single or Essay

```json
{
    "headings": [
        {
            "heading": "What's your favorite thing about monkeys?"
        }
    ],
    "position": 1,
    "family": "open_ended",
    "subtype": "single"
}
```
![Open Ended Single](https://raw.githubusercontent.com/SurveyMonkey/public_api_docs/master/images/open-ended-single.png)

Only requires a `heading`.

####Open Ended - Multi

>Open Ended - Multi

```json
{
    "headings": [
        {
            "heading": "What are your favorite monkey species?"
        }
    ],
    "position": 1,
    "family": "open_ended",
    "subtype": "multi",
    "answers": {
        "rows":[
            {
                "text": "Your favorite:"
            },
            {
                "text": "Second favorite:"
            }
        ]
    }
}
```
![Open Ended Multi](https://raw.githubusercontent.com/SurveyMonkey/public_api_docs/master/images/open-ended-multi.png)

Name | Description | data Type
----- | ------ | -----
rows (required) | List of textboxes | Array
rows[\_].text (required) | Text label for textbox | String
rows[\_].position (optional) | Position of the current row | Integer

####Open Ended - Numerical

>Open Ended - Numerical

```json
{
    "headings": [
        {
            "heading": "If you could split 10 pounds of ice cream, how would you split it?"
        }
    ],
    "position": 1,
    "family": "open_ended",
    "subtype": "numerical",
    "answers": {
        "rows":[
            {
                "text": "Pounds for family:"
            },
            {
                "text": "Pounds for friends:"
            },
            {
                "text": "Pounds for self:"
            }
        ]
    },
    "validation": {
        "text": "Please enter a valid integer.",
        "type": "integer",
        "sum": 10,
        "sum_text": "Your input must add up to 10 pounds!"
    }
}
```
![Open Ended Numerical](https://raw.githubusercontent.com/SurveyMonkey/public_api_docs/master/images/open-ended-numerical.png)

Name | Description | Data Type
----- | ------ | -----
rows (required) | List of textboxes | Array
rows[\_].text (required) | Text label for textbox | String
rows[\_].position (optional) | Position of the current row | Integer


####Demographic

>Demographic

```json
{
    "headings": [
        {
            "heading": "What's your address?"
        }
    ],
    "position": 1,
    "visible": true,
    "family": "demographic",
    "subtype": "international",
    "answers": {
        "rows": [
            {
                "visible": true,
                "required": true,
                "type": "name",
                "text": "Your Name"
            },
            {
                "visible": true,
                "required": false,
                "type": "company"
            },
            {
                "visible": false,
                "required": false,
                "type": "address"
            },
            {
                "visible": false,
                "required": false,
                "type": "address2"
            },
            {
                "visible": true,
                "required": true,
                "type": "city"
            },
            {
                "visible": true,
                "required": true,
                "type": "state"
            },
            {
                "visible": true,
                "required": true,
                "type": "zip"
            },
            {
                "visible": true,
                "required": true,
                "type": "country"
            },
            {
                "visible": true,
                "required": true,
                "type": "email"
            },
            {
                "visible": true,
                "required": true,
                "type": "phone"
            }
        ]
    }
}
```
![Demographic](https://raw.githubusercontent.com/SurveyMonkey/public_api_docs/master/images/demographic.png)

This corresponds to the **Contact Information** question type in the SurveyMonkey UI.

Each `type` represented in the example object must be included, to disable one, specify `visible` as `False`

Name | Description | Data Type
----- | ------ | -----
rows | List of available demographic data | Array
rows[\_].visible (required) | Visibility of demographic data type | Boolean
rows[\_].required (required) | Whether demographic data type is required | Boolean
rows[\_].type (required) | Type of demographic data | String
rows[\_].text (optional) | Optional label of demographic data, will default to type | String


####DateTime

>DateTime

```json
{
    "headings": [
        {
            "heading": "When did you last eat ice cream?"
        }
    ],
    "position": 1,
    "visible": true,
    "family": "datetime",
    "subtype": "both",
    "answers": {
        "rows": [
            {
                "text": "At:",
                "position": 1
            }
        ]
    }
}
```
![DateTime](https://raw.githubusercontent.com/SurveyMonkey/public_api_docs/master/images/datetime.png)

Name | Description | Data Type
----- | ------ | -----
rows[\_].text (required) | Label for date/time input box | String
rows[\_].position (optional) | Position of date/time input box | Integer

####Presentation 

>Presentation

```json
{
    "headings": [
        {
            "heading": "This is a monkey",
            "image": {
                "url": "http://surveymonkey.com/monkey.jpg"
            }
        }
    ],
    "position": 1,
    "family": "presentation",
    "subtype": "image"
}
```
![Presentation](https://raw.githubusercontent.com/SurveyMonkey/public_api_docs/master/images/presentation.png)

If `image` is included, this corresponds to the **Image** question type in the SurveyMonkey UI. If not included, it corresponds to the **Text** question type.

Name | Description | Data Type
----- | ----- | -----
 image (optional)| Image to present| Object
 image[\_].image_url (required)| URL of image to present | String |

####File Upload

>File Upload

```json
{
    "headings": [
        {
            "heading": "Upload your favorite monkey picture."
        }
    ],
    "position": 1,
    "family": "open_ended",
    "subtype": "single",
    "display_options": {
        "display_type": "file_upload"
    }
}
```

![File Upload](https://raw.githubusercontent.com/SurveyMonkey/public_api_docs/master/images/file-upload.png)

A open ended single answer with the `display_options` object can become a [File Upload](https://help.surveymonkey.com/articles/en_US/kb/File-Upload-Question)
question.

Name | Description | Data Type
----- | ----- | -----
 display_options[\_].display_type (required)| Turns an open ended, single answer question into a file upload question. Always `file_upload` | String-ENUM |

####Slider

>Slider

```json
{
    "headings": [
        {
            "heading": "On a scale of 1 to 100, how much do you like monkeys?"
        }
    ],
    "position": 1,
    "family": "open_ended",
    "subtype": "single",
    "display_options": {
        "display_type": "slider"
    }
}
```

>Slider Complex

```json
{
    "headings": [
        {
            "heading": "On a scale of 1 to 100, how much do you like monkeys?"
        }
    ],
    "position": 1,
    "family": "open_ended",
    "subtype": "single",
    "display_options": {
      "right_label": "",
      "display_type": "slider",
      "custom_options": {
        "starting_position": 0,
        "step_size": 1
      },
      "left_label": ""
    },

    "validation": {
      "sum_text": "",
      "min": 45,
      "text": "Please enter a whole number between {0} and {1}.",
      "max": 10000,
      "type": "integer"
    }
}
```
![Slider](https://raw.githubusercontent.com/SurveyMonkey/public_api_docs/master/images/slider.png)

A open ended single answer with the `display_options` object can become a [slider](https://help.surveymonkey.com/articles/en_US/kb/Slider)
question.

Name | Description | Data Type
----- | ----- | -----
display_options[\_].display_type (required)| Turns an open ended single answer question into a slider question. Always `slider` | String-ENUM |
display_options[\_].right_label (optional)|Label to place at the right end of the slider|String|
display_options[\_].left_label (optional)|Label to place at the left end of the slider|String|
display_options[\_].custom_options[\_].starting_position (optional)|Where the slider marker is positioned by default|Integer
display_options[\_].custom_options[\_].step_size (optional)|Step size the slider increments when moved|Integer

####Emoji (Star Rating)

>Emoji (Star Rating)

```json
{
    "headings": [
        {
            "heading": "How many stars on the walk of fame should monkeys have?"
        }
    ],
    "position": 1,
    "family": "matrix",
    "subtype": "rating",
    "display_options": {
        "display_type": "emoji",
        "display_subtype": "star"
    },
    "forced_ranking": false,
    "answers":{
    "rows": [
      {
        "visible": true,
        "text": "",
        "position": 1
      }
    ],
    "choices": [
      {
        "weight": 1,
        "text": ""
      },
      {
        "weight": 2,
        "text": ""
      },
      {
        "weight": 3,
        "text": ""
      },
      {
        "weight": 4,
        "text": ""
      },
      {
        "weight": 5,
        "text": ""
      }
    ]
  }
}
```
![emoji (star rating)](https://raw.githubusercontent.com/SurveyMonkey/public_api_docs/master/images/star-rating.png)

A rating question with the `display_options` object can become an emoji or [Star Rating](https://help.surveymonkey.com/articles/en_US/kb/Star-Rating) question.

Name | Description | Data Type
----- | ----- | -----
 display_options[\_].display_type (required)| Turns and open ended single answer question into an emoji question. Always `emoji`|String-ENUM|
 display_options[\_].display_subtype (required)| Which emoji is displayed: `star`, `smiley`, `heart`, or `thumb`|String-ENUM|

