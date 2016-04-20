##Collectors and Invite Messages

Collectors allow you to collect survey responses with a link to your survey. There are two `types` of collectors available via the API, `weblink` and `email`. [Weblink collectors](http://help.surveymonkey.com/articles/en_US/kb/Web-Link-Collector) collectors give you a survey URL and email collectors can be used to send survey invites messages that include a survey URL via the /messages endpoints. A variety of [collector options](http://help.surveymonkey.com/articles/en_US/kb/Collector-Options#List) are accepted as arguments to /surveys/{id}/collectors. Some collector options, for example, `is_branding_enabled=False` require a [SurveyMonkey paid plan]((https://www.surveymonkey.com/pricing/?ut_source=dev_portal&amp;ut_source2=docs)). 


###/surveys/{id}/collectors

>Definition

```
POST https://api.surveymonkey.net/v3/surveys/{survey_id}/collectors
```
>Example Request

```shell
curl -i -X POST -H "Authorization:bearer YOUR_ACCESS_TOKEN" https://api.surveymonkey.net/v3/survey/1234/collectors?api_key=YOUR_API_KEY -d '{"type":"weblink"}'
```

```python
import requests

s = requests.session()

payload = {
 'type': 'weblink'
}
url = "https://api.surveymonkey.net/v3/surveys/%s/collectors?api_key=%s" % (survey_id, YOUR_API_KEY)
s.post(url, data=payload)
```

>Example Response

```json
{
  "status": "open",
  "id": "1234",
  "type": "weblink",
  "name": "My Collector",
  "thank_you_message": "Thank you for taking my survey.",
  "disqualification_message": "Thank you for taking my survey.",
  "close_date": "2038-01-01T00:00:00+00:00",
  "closed_page_message": "This survey is currently closed.",
  "redirect_url": "https://www.surveymonkey.com",
  "display_survey_results": false,
  "edit_response_type": "until_complete",
  "anonymous_type": "not_anonymous",
  "allow_multiple_responses": false,
  "date_modified": "2015-10-06T12:56:55+00:00",
  "url": "https://www.surveymonkey.com/r/2Q3RXZB",
  "open": true,
  "date_created": "2015-10-06T12:56:55+00:00",
  "password_enabled": false,
  "href": "https://api.surveymonkey.net/v3/collectors/1234"
}
```

 * `HEAD`: Checks if resource is available
 * `OPTIONS`: Returns available methods and options
 * `GET`: Returns a list of collectors for a given survey
 * `POST`: Creates a [weblink](http://help.surveymonkey.com/articles/en_US/kb/Web-Link-Collector) or [email collector](http://help.surveymonkey.com/articles/en_US/kb/Email-Invitation-Collector) for a given survey

####Optional Query Strings for GET

Name | Description | Type
------ | ------- | -------
page | Which page of resources to return. Defaults to 1 | Integer
per_page | Number of resources to return per page | Integer
sort_by | Field used to sort returned collector list e.g. ['id', 'date_modified', 'type', 'status', 'name'] | String-ENUM
sort_order | Sort order e.g. ['ASC', 'DESC'] | String-ENUM
name | Nickname of collector to search against | String
start_date | Collectors must be created after this date. | Date String
end_date | Collectors must be created before this date. | Date String

####Collector List Resource

Name | Description | Type
------ | ------- | -------
data[_].id| Collector id | String
data.name | Collector name | String
data.href | Resource API URL | String

 
####Request Body Arguments for POST

Name | Required |Description | Type
------ | ------- | ------- | -------
type | Yes | Collector type: 'weblink' or 'email'| String-ENUM
name | No | Collector name | String
thank_you_message | No (default="Thank you for completing our survey!"")| Message for [thank you page](http://help.surveymonkey.com/articles/en_US/kb/Can-I-create-a-Thank-You-page)  | String-ENUM
disqualification_message | No (default="Thank you for completing our survey!)| Message for disqualification page  | String-ENUM
close_date | No | Close date of collector | Date String
closed_page_message | No (default="Thank you for completing our survey!") | Message shown when a survey is closed| String-ENUM
redirect_url | No | Redirect to this url upon survey completion | String
display_survey_results | No (default=False) | Shows respondents survey [instant results](http://help.surveymonkey.com/articles/en_US/kb/What-are-Instant-Results) when they complete the survey | Boolean
edit_response_type | No (default='until_complete') | When respondents can edit their response:'until_complete', 'never', or 'always' | String-ENUM
anonymous_type | No (default='not_anonymous') | Turns off IP tracking. For email collectors, also removes respondent email address and name from response: 'not_anonymous', 'partially_anonymous', 'fully_anonymous' | String-ENUM
allow_multiple_responses |  No (default=False) | Allows respondents to take a survey more than once from the same browser on the same computer | Boolean
password | No | Set a password to restrict access to your survey | String

###/collectors/{id}

>Definition

```
GET https://api.surveymonkey.net/v3/collectors/{collector_id}
```

>Example Request

```shell
curl -i -X GET -H "Authorization:bearer YOUR_ACCESS_TOKEN" https://api.surveymonkey.net/v3/collectors/1234?api_key=YOUR_API_KEY
```

```python
import requests

s = requests.session()

url = "https://api.surveymonkey.net/v3/collectors/%s?api_key=%s" % (collector_id, YOUR_API_KEY)
s.get(url)
```

>Example Response

```json
{
  "status": "open",
  "id": "1234",
  "type": "weblink",
  "name": "My Collector",
  "thank_you_message": "Thank you for taking my survey.",
  "disqualification_message": "Thank you for taking my survey.",
  "close_date": "2038-01-01T00:00:00+00:00",
  "closed_page_message": "This survey is currently closed.",
  "redirect_url": "https://www.surveymonkey.com",
  "display_survey_results": false,
  "edit_response_type": "until_complete",
  "anonymous_type": "not_anonymous",
  "allow_multiple_responses": false,
  "date_modified": "2015-10-06T12:56:55+00:00",
  "url": "https://www.surveymonkey.com/r/2Q3RXZB",
  "date_created": "2015-10-06T12:56:55+00:00",
  "href": "https://api.surveymonkey.net/v3/collectors/1234"
}
```

####Available Methods

 * `HEAD`: Checks if resource is available
 * `OPTIONS`: Returns available methods and options
 * `GET`: Returns a collector
 * `PATCH`: Modifies a collector (updates any fields accepted as arguments to `POST` [/surveys/{survey_id}/collectors](#surveys-id-collectors), with the addition of `status` and the removal of `type`)
 * `PUT`: Replaces a collector (same arguments and requirements as `POST`[/surveys/{survey_id}/collectors](#surveys-id-collectors), with the addition of `status` and the removal of `type`)
 * `DELETE`: Deletes a collector


####Collector Resource

Name | Description | Type
------ | ------- | -------
status | Collector status: 'open' or 'closed'| String
id | Collector id | String
type | Collector type: 'weblink' or 'email' | String
name | Name of the collector | String
thank_you_message | Message for thank you page | String
disqualification_message | Message for disqualification page | String
close_date  | Close date of collector | Date String
closed_page_message | Message for close page | String
redirect_url | Redirect to this url upon survey completion. | String
display_survey_results | Shows respondents survey [instant results](http://help.surveymonkey.com/articles/en_US/kb/What-are-Instant-Results) when they complete the survey | Boolean
edit_response_type | When respondents can edit their response: 'until_complete', 'never', or 'always' | String
anonymous_type | Turns off IP tracking. For email collectors, also removes respondent email address and name from response: 'not_anonymous', 'partially_anonymous', 'fully_anonymous' | String
allow_multiple_responses| Allows respondents to take a survey more than once from the same browser on the same computer | Boolean
date_modified | Date collector was last modified | Date String
url | If collector is a Web Collector (type 'weblink') then the url for the collector | String
date_created | Date collector was created | Date String
href | Resource API URL | String


###/collectors/{id}/messages

>Definition

```
POST https://api.surveymonkey.net/v3/collectors/{collector_id}/messages
```

>Example Request

```shell
curl -i -X POST -H "Authorization:bearer YOUR_ACCESS_TOKEN" https://api.surveymonkey.net/v3/collectors/1234/messages?api_key=YOUR_API_KEY -d '{"subject":"Please help me by taking my survey", "body_text":"Thank you in advance for taking my survey. [SurveyLink], [OptOutLink], [FooterLink]","is_branding_enabled":True}'
```

```python
import requests

s = requests.session()

payload = {
  'subject': 'Please help me by taking my survey',
  'body_text': 'Thank you in advance for taking my survey. [SurveyLink], [OptOutLink], [FooterLink]',
  'is_branding_enabled': True,
  'type': 'invite'
}
url = "https://api.surveymonkey.net/v3/collectors/%s/messages?api_key=%s" % (collector_id, YOUR_API_KEY)
s.post(url)
```

>Example Response

```json
{
    "status": "not_sent",
    "is_scheduled": false,
    "subject": "Please help me by taking my survey",
    "body": "Thank you in advance for taking my survey. [SurveyLink], [OptOutLink], [FooterLink]",
    "is_branding_enabled": true,
    "date_created": "2015-10-06T12:56:55+00:00",
    "type": "invite",
    "id": "1234",
    "href": "https://api.surveymonkey.net/v3/collectors/1234/messages/2345"
}
```

 * `HEAD`: Checks if resource is available
 * `OPTIONS`: Returns available methods and options
 * `GET`: Returns a message
 * `POST`: Creates a message. See [/collectors/{id}/messages/{id}/recipients](#collectors-id-messages-id-recipients) to add recipients and [/collectors/{id}/messages/{id}/send](#collectors-id-messages-id-send) to send or schedule

####Optional Query Strings for GET

Name | Description | Type
------ | ------- | -------
page | Which page of resources to return. Defaults to 1 | Integer
per_page | Number of resources to return per page | Integer

####Request Body Arguments for POST

Name | Required |Description | Type
------ | ------- | ------- | -------
type | Yes | Message type: 'invite', 'reminder', or 'thank_you' | String-ENUM
recipient_status | No. If type is 'reminder', acceptable values are: 'has_not_responded' or 'partially_responded', with the default being 'has_not_responded'. If type is 'thank_you', acceptable values are :'completed', 'responded', or 'partially_responded', with the default being 'completed' | Set of recipients to send to | String-ENUM  
subject | No (default="Please help me by taking my survey") | Subject of the email message to be sent to recipients | String
body_text | No (default="Thank you in advance for taking my survey. [SurveyLink], [OptOutLink], [FooterLink]")| The plain text body of the email message to be sent to recipients. Message must include [SurveyLink], [OptOutLink], and [FooterLink] | String
body_html | No (default="Thank you in advance for taking my survey. [SurveyLink], [OptOutLink], [FooterLink]")| The html body of the email message to be sent to recipients. This overrides body_text. Message must include [SurveyLink], [OptOutLink], and [FooterLink] | String
is_branding_enabled | No (default=True) | Whether the email has SurveyMonkey branding  | Boolean


###/collectors/{id}/messages/{id}

<aside class="notice">
Only subject, body_text, body_html, is_branding, and recipient_status if 'reminder' or 'thank_you', can be modified with PUT and PATCH.
</aside>

>Definition

```
GET https://api.surveymonkey.net/v3/collectors/{collector_id}/messages/{message_id}
```

>Example Request

```shell
curl -i -X GET -H "Authorization:bearer YOUR_ACCESS_TOKEN" https://api.surveymonkey.net/v3/collectors/1234/messages/1234?api_key=YOUR_API_KEY
```

```python
import requests

s = requests.session()

url = "https://api.surveymonkey.net/v3/collectors/%s/messages/%s?api_key=%s" % (collector_id, message_id, YOUR_API_KEY)
s.get(url)
```
>Example Response

```json
{
    "status": "not_sent",
    "is_scheduled": true,
    "subject": "Email subject",
    "body": "Email body",
    "is_branding_enabled": true,
    "date_created": "2015-10-06T12:56:55+00:00",
    "scheduled_date": "2015-10-07T12:56:55+00:00",
    "type": "invite",
    "recipient_status": null,
    "id": "1234",
    "href": "https://api.surveymonkey.net/v3/collectors/1234/messages/1234"
}
```
####Available Methods

 * `HEAD`: Checks if resource is available
 * `OPTIONS`: Returns available methods and options
 * `GET`: Returns a message
 * `PATCH`: Modifies a message (only subject, body_text, body_html, is_branding, and recipient_status if 'reminder' or 'thank_you', can be modified)
 * `PUT`: Replaces a message (only subject, body_text, body_html, is_branding, and recipient_status if 'reminder' or 'thank_you', can be modified)
 * `DELETE`: Deletes a message 

####Messages Resource

Name | Description | Type
------ | ------- | -------
status | Whether the message is: 'sent', 'not_sent', or 'processing'| String
is_scheduled | If a message has been secheduled to send. See [/collectors/{id}/messages/{id}/send](#collectors-id-messages-id-send) | Boolean
is_branding_enabled | Whether the email has SurveyMonkey branding | Boolean
date_created | Date message was created | Date String
scheduled_date | Date message was scheduled to be sent | Date String
type | Message type: 'invite', 'reminder', or 'thank_you' | String
recipient_status | Recipient filter: 'reminder' or 'thank_you' | String 
id | Message id | String


###/collectors/{id}/messages/{id}/send


>Definition

```
POST https://api.surveymonkey.net/v3/collectors/{collector_id}/messages/{message_id}/send 
```

>Example Request

```shell
curl -i -X POST -H "Authorization:bearer YOUR_ACCESS_TOKEN" https://api.surveymonkey.net/v3/collectors/1234/messages/1234/send?api_key=YOUR_API_KEY -d '{"scheduled_date":"2015-10-06T12:56:55+00:00"}'
```

```python
import requests

s = requests.session()

payload = {
  'scheduled_date': '2015-10-06T12:56:55+00:00'
}
url = "https://api.surveymonkey.net/v3/collectors/%s/messages/%s/send?api_key=%s" % (collector_id, message_id, YOUR_API_KEY)
s.post(url, data=payload)
```

>Example Request

```json
{
    "scheduled_date": "2015-10-06T12:56:55+00:00"
}
```

>Example Response

```json
{
  "is_scheduled": true,
  "scheduled_date": "2015-11-04T12:56:55+00:00",
  "body": "<html>...</html>",
  "subject": "We want your opinion",
  "recipients": ["41930647", "41930648"],
  "recipient_status": null,
  "type": "invite"
}
```
####Available Methods

 * `POST`: Send or schedule to send an existing message to all message recipients that have not received the message. See [/collectors/{id}/messages/{id}/recipients](#collectors-id-messages-id-recipients) to add recipients

####Request Body Arguments for POST

Name | Required | Description | Type
------ | ------- | ------- | -------
scheduled_date | No | Date when the message should send. If not specified, message sends immediately | Date String

####Message Resource 

Name | Description | Type
------ | ------- | -------
is_scheduled | If a message has been secheduled to send | Boolean
scheduled_date | Date message was scheduled to be sent | Date String
body | The plain text body of the email message to be sent to recipients. | String
subject | Subject of the email message to be sent to recipients | String
recipients | List of recipient ids | Array
type | Message type: 'invite', 'reminder', or 'thank_you' | String
recipient_status | Recipient filter: 'reminder' or 'thank_you' | String 

###/collectors/{id}/messages/{id}/recipients

<aside class="notice">
If the contact_id is provided, fetch the contact from the address book. If contact_id is not provided, allow passing of the email, name, and custom_fields. A new contact will only be created if an existing contact with the same email cannot be found. If custom_fields are provided, update the contact with those fields, otherwise keep existing custom_fields. 
</aside>

>Definition

```
POST https://api.surveymonkey.net/v3/collectors/{collector_id}/messages/{message_id}/recipients
```

>Example Request (with contact_id)

```shell
curl -i -X POST -H "Authorization:bearer YOUR_ACCESS_TOKEN" https://api.surveymonkey.net/v3/collectors/1234/messages/1234/recipients?api_key=YOUR_API_KEY -d '{"contact_id:"1234"}'
```

```python
import requests

s = requests.session()

payload = {
  'contact_id': 1234
}
url = "https://api.surveymonkey.net/v3/collectors/%s/messages/%s/recipients?api_key=%s" % (collector_id, message_id, YOUR_API_KEY)
s.post(url, data=payload)
```

>Example Request (without contact_id)

```shell
curl -i -X POST -H "Authorization:bearer YOUR_ACCESS_TOKEN" https://api.surveymonkey.net/v3/collectors/1234/messages/1234/recipients?api_key=YOUR_API_KEY -d '{"email":"test@surveymonkey.com"}'
```

```python
import requests

s = requests.session()

payload = {
  "email": "test@surveymonkey.com",
  "first_name": "John",
  "last_name": "Doe",
  "custom_fields": {
    "1": "Mr",
    "2": "Company",
    "3": "Address",
    "4": "City",
    "5": "Country",
    "6": "Phone Number"
  },
  "extra_fields": [
      "favorite_color": "Red",
      "second_favorite_color": "Black",
      "third_favorite_color": "Green"
  ]
}
url = "https://api.surveymonkey.net/v3/collectors/%s/messages/%s/recipients?api_key=%s" % (collector_id, message_id, YOUR_API_KEY)
s.post(url, data=payload)
```

>Example Response

```json
{
    "survey_response_status": "not_responded",
    "mail_status": "not_sent",
    "email": "test@surveymonkey.com",
    "first_name": "John",
    "last_name": "Doe",
    "custom_fields": {
      "1": "Mr",
      "2": "Company",
      "3": "Address",
      "4": "City",
      "5": "Country",
      "6": "Phone Number"
    },
    "id": "1234",
    "remove_link": "https://www.surveymonkey.com/optout.aspx?sm=1234",
    "extra_fields": {
        "favorite_color": "Red",
        "second_favorite_color": "Black",
        "third_favorite_color": "Green"
    },
    "survey_link": "https://www.surveymonkey.com/r/?sm=1234",
    "href": "https://api.surveymonkey.net/v3/collectors/1234/recipients/1234"
}
```

####Available Methods

 * `HEAD`: Checks if resource is available
 * `OPTIONS`: Returns available methods and options
 * `GET`: Returns a list of recipients
 * `POST`: Creates a new recipient for the specified message. See [/collectors/{id}/messages/{id}/send](#collectors-id-messages-id-send) for sending. This method only available to messages of type `invite` if they have not already been sent

####Optional Query Strings for GET

Name | Description | Type
------ | ------- | -------
page | Which page of resources to return. Defaults to 1 | Integer
per_page | Number of resources to return per page | Integer

####Recipient List Resource

Name | Description | Type
------ | ------- | -------
data.id | Recipient id | String
data.email | Email of recipient added to collector | String

####Requests Body Arguments for POST (if passing contact_id)

Name |  Required |Description | Type
------ | ------- | ------- | -------
contact_id | Yes | Contact id | String

####Requests Body Arguments for POST (if not passing contact_id)

Name |  Required |Description | Type
------ | ------- | ------- | -------
email | Yes  | Email of the recipient | String
first_name | No | First name of the recipient | String
last_name | No | Last name the recipient | String
custom_fields | No | Custom fields for the recipient contact | Dictionary
extra_fields | No | Extra fields needed for the message body | Dictionary


###/collectors/{id}/messages/{id}/recipients/bulk

>Definition

```
POST https://api.surveymonkey.net/v3/collectors/{collector_id}/messages/{message_id}/recipients/bulk
```

<aside class="notice">
If custom_fields are provided for any one contact, all contacts will have their custom_fields updated. In other words, if contact_1's custom_fields is provided, but contact_2's custom_fields is not provided, contact_2's previous custom_fields will be cleared after this API call.
</aside>

>Example Request

```shell
curl -i -X POST -H "Authorization:bearer YOUR_ACCESS_TOKEN" https://api.surveymonkey.net/v3/collectors/1234/messages/1234/recipients/bulk?api_key=YOUR_API_KEY -d '{"contact_ids":["1234", "5678"]}'
```

```python
import requests

s = requests.session()

payload = {
  "contact_ids": ["1234", "5678"],
  "contact_list_ids": ["1234567", "4567890"],
  "contacts" :[{
      "email":"test@surveymonkey.com",
      "first_name": "John",
      "last_name": "Doe",
      "custom_fields": {
        "1": "Mr",
        "2": "Company",
        "3": "Address",
        "4": "City",
        "5": "Country",
        "6": "Phone Number"
      },
      "extra_fields": {
        "favorite_color": "Red",
        "second_favorite_color": "Black"
      }
  }]
}
url = "https://api.surveymonkey.net/v3/collectors/%s/messages/%s/recipients?api_key=%s" % (collector_id, message_id, YOUR_API_KEY)
s.post(url, data=payload)
```
>Example Response

```json
{
  "succeeded": [{
    "id": "1234",
    "email": "test@surveymonkey.com",
    "href": "https://api.surveymonkey.net/v3/collectors/1234/recipients/1234"
  }],
  "invalids": [],
  "existing": [],
  "bounced": [],
  "opted_out": [],
  "duplicate": []
}
```

####Available Methods

 * `POST`: Creates multiple recipients

####Request Body Arguments for POST

Name |  Required |Description | Type
------ | ------- | ------- | -------
data[\_].contact_ids | No | Contact ids | Array
data[\_].contact_list_ids | No | Contact list ids | Array
data[_].email | No | Contact emails | String
data[\_].first_name | No | Contact's first name | String
data[\_].last_name  | No | Contact's last name | String
data[\_].custom_fields | No | Custom fields for contact | Dictionary
data[\_].extra_fields | No | Extra fields needed for the message body | Dictionary

####Bulk Response

Name |Description | Type
------ | ------- | -------
succeeded | Successfully added recipients | Array
invalids | Invalid recipients that were provided | Array
existing | Recipients that have already been added | Array
bounced | Recipients that have previously bounced | Array
opted_out | Recipientents that have opted out of recieving emails | Array
duplicate | Duplicate recipients that were provided | Array

###/collectors/{id}/recipients/{id}

>Definition

```
GET https://api.surveymonkey.net/v3/collectors/{collector_id}/recipients/{recipient_id}
```
>Example Request

```shell
curl -i -X GET -H "Authorization:bearer YOUR_ACCESS_TOKEN" https://api.surveymonkey.net/v3/collectors/1234/recipients/1234?api_key=YOUR_API_KEY
```

```python
import requests

s = requests.session()
#See Requests Guide for Setting Up Requests Session

url = "https://api.surveymonkey.net/v3/collectors/%s/recipients/%s?api_key=%s" % (collector_id, message_id, recipient_id, YOUR_API_KEY)
s.get(url)
```

>Example Response

```json
{
    "first_name": "John",
    "last_name": "Doe",
    "email": "test@surveymonkey.com",
    "survey_response_status": "not_responded",
    "mail_status": "not_sent",
    "custom_fields": {
      "1": "Mr",
      "2": "Company",
      "3": "Address",
      "4": "City",
      "5": "Country",
      "6": "Phone Number"
    },
    "id": "1234",
    "remove_link": "https://www.surveymonkey.com/optout.aspx?sm=1234",
    "extra_fields": {
        "favorite_color": "Red",
        "second_favorite_color": "Black",
        "third_favorite_color": "Green"
    },
    "survey_link": "https://www.surveymonkey.com/r/?sm=1234"
}
```
####Available Methods

 * `HEAD`: Checks if resource is available
 * `OPTIONS`: Returns available methods and options
 * `GET`: Returns a recipient
 * `DELETE`: Deletes a recipient

####Recipient Resource

Name | Description | Type
------ | ------- | -------
survey_response_status | If the recipient has completed the survey: 'not_responded', 'partially_responded', 'completely_responded'| String
mail_status | If an invite message to the recipient has been: 'sent', 'not_sent', or is 'processing' | String
custom_fields | Contact details for recipient | Dictionary
id | Recipient's id | String
remove_link | Unsubscribe link | String
extra_fields | Extra fields | Dictionary
survey_link | Link to the survey | String






