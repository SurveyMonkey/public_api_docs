##Webhooks

Create webhooks that subscribe to various events in SurveyMonkey. You can create a webhook to callback when:


 * A survey response is completed ('response_completed')
 * A survey response is [disqualified](http://help.surveymonkey.com/articles/en_US/kb/Disqualifying-Respondents) ('response_disqualified')
 * A survey response is updated ('response_updated')
 * A respondent begins a survey ('response_created')
 * A response is deleted ('response_deleted')
 * A response is over a [survey's quota](https://help.surveymonkey.com/articles/en_US/kb/What-are-Quotas) ('response_overquota')
 * A collector is created ('collector_created')
 * A collector is updated ('collector_updated')
 * A collector is deleted ('collector_deleted')

You can specify one or more survey ids to be included.

###/webhooks

>Definition

```
POST https://api.surveymonkey.net/v3/webhooks
```

>Example Request

```shell
curl -X POST -H "Authorization:bearer YOUR_ACCESS_TOKEN" -H "Content-Type": "application/json" https://api.surveymonkey.net/v3/webhooks -d \
  '{"name":"My Webhook", "event_type":"response completed", "object_type":"survey", "object_ids":["1234","5678"],"subscription_url":"https://surveymonkey.com/webhook_reciever"}'
```

```python
import requests

s = requests.session()
s.headers.update({
  "Authorization": "Bearer %s" % YOUR_ACCESS_TOKEN,
  "Content-Type": "application/json"
})

payload = {
  "name": "My Webhook",
  "event_type": "response_completed",
  "object_type": "survey",
  "object_ids": ["1234", "5678"],
  "subscription_url": "https://surveymonkey.com/webhook_reciever"
}
url = "https://api.surveymonkey.net/v3/webhooks"
s.post(url, json=payload)
```

>Example Response

```json
{
  "id": "1234",
  "name": "My Webhook",
  "event_type": "response_completed",
  "object_type": "survey",
  "object_ids": ["1234", "5678"],
  "subscription_url": "https://surveymonkey.com/webhook_reciever",
  "href": "https://api.surveymonkey.net/v3/webhooks/123"
}
```
####Available Methods

 * `HEAD`: Checks if resource is available
 * `OPTIONS`: Returns available methods and options
 * `GET`: Returns a list of webhooks. Public App users need access to the **View Webhooks** [scope](#scopes)
 * `POST`: Create a webhook, see below for callback format. Public App users need access to the **Create/Modify Webhooks** [scope](#scopes)

####Optional Query Strings for GET

Name | Description | Data Type
------ | ------- | -------
page | Which page of resources to return. Defaults to 1 | Integer
per_page | Number of resources to return per page | Integer

####Webooks List Resource

Name | Description | Data Type
------ | ------- | -------
data[\_].id | Webhook id | String
data[\_].name | Webhook name | String
data[\_].href | Resource API URL | String

####Request Body Arguments for POST

Name | Required | Description | Data Type
------ | ------- | ------- | -------
name | Yes | Webhook name | String
event_type | Yes | Event type that the webhook listens to: `response_completed`, `response_updated`, `response_disqualified`, `response_created`, `response_deleted`, `response_overquota`, `collector_created`, `collector_updated`, `collector_deleted`. | String-ENUM
object_type | Yes | Object type to filter events by: `survey` or `collector`. NOTE: Setting `object_type` to `collector` and `event_type` to `collector_created` will result in a 400 error.| String-ENUM
object_ids | Yes | Object ids to filter events by (for example, survey ids to listen for the `response_completed` event) | Array
subscription_url | Yes. Url must accept a HEAD request and return a 200.  | Subscription url that events are sent to | String


###/webhooks/{id}

>Definition

```
GET https://api.surveymonkey.net/v3/webhooks/{webhook_id}
```

>Example Request

```shell
curl -H "Authorization:bearer YOUR_ACCESS_TOKEN" -H "Content-Type": "application/json" https://api.surveymonkey.net/v3/webhooks/1234
```

```python
import requests

s = requests.session()
s.headers.update({
  "Authorization": "Bearer %s" % YOUR_ACCESS_TOKEN,
  "Content-Type": "application/json"
})

url = "https://api.surveymonkey.net/v3/webhooks/%s" % (webhook_id)
s.get(url)
```

>Example Response

```json
{
  "id": "1234",
  "name": "My Webhook",
  "event_type": "response_completed",
  "object_type": "survey",
  "object_ids": ["1234", "5678"],
  "subscription_url": "http://requestb.in/13qm6kg1",
  "href": "https://api.surveymonkey.net/v3/webhooks/123"
}
```

####Available Methods

 * `HEAD`: Checks if resource is available
 * `OPTIONS`: Returns available methods and options
 * `GET`: Returns a webhook. Public App users need access to the **View Webhooks** [scope](#scopes)
 * `PATCH`: Modifies a webhook (updates any fields accepted as arguments to `POST` [/webhooks](#webhooks)). Public App users need access to the **Create/Modify Webhooks** [scope](#scopes)
 * `PUT`: Replaces a webhook (same arguments and requirements as `POST` [/webhooks](#webhooks)). Public App users need access to the **Create/Modify Webhooks** [scope](#scopes)
 * `DELETE`: Deletes a webhook. Public App users need access to the **Create/Modify Webhooks** [scope](#scopes)

####Webhook Resource

Name | Description | Data Type
------ | ------- | -------
id  | Webhook id | String
name  | Webhook name | String
event_type | Event type that the webhook listens to: `response_completed`, `response_disqualified`, or `response_updated` | String-ENUM
object_type | Object type to filter events by: `survey` or `collector` | String-ENUM
object_ids | Object ids to filter events by (for example, survey ids to listen for the `response_completed` event) | Array
subscription_url | Subscription url that callback events are sent to | String
href | Resource API URL | String

###Webhook Callbacks

Our webhook callbacks include the following request headers that can be used to verify the request is coming from SurveyMonkey:

 * Sm-Apikey: Your Client ID or API key (if you're using [OLD Authentication](#old-authentication))
 * Sm-Signature: # HMAC digest hashed with sha1 

>Verifying the request

```python 

import hashlib
import hmac
import base64
 
def generate_signature(payload, api_key, api_secret):

"""
:type payload: str The response body from the webhook exactly as you received it
:type api_key: str Your API Key for you app (if you have one) otherwise your Client ID
:type api_secret: str Your API Secret for your app
:return: str
"""
 
# ensure all strings passed in are ascii strings,
# as hmac does not work on unicode

api_key = api_key.encode("ascii")
api_secret = api_secret.encode("ascii")
payload = payload.encode("ascii")
 
signature = hmac.new(
key='%s&%s' % (api_key, api_secret),
msg=payload,
digestmod=hashlib.sha1)
 
signature_digest = signature.digest()
 
return base64.b64encode(signature_digest)
 
# Compare the signature generated from the request body against the one in the request headers
hmac.compare_digest(generate_signature(request.body, api_key, api_secret), request.headers['Sm-Signature'])
```

>Example Collector Event Data

```json
{
  "name": "My Webhook",
  "filter_type": "survey",
  "filter_id": "123456789",
  "event_type": "response_completed",
  "event_id": "123456789",
  "object_type": "response",
  "object_id": "123456",
  "event_datetime": "2016-01-01T21:56:31.182613+00:00",
  "resources": {
    "collector_id": "123456789",
    "survey_id": "123456789",
    "user_id": "123456789"
  }
}
```
>Example Response Event Data

```json
{
  "name": "My Webhook",
  "filter_type": "collector",
  "filter_id": "123456789",
  "event_type": "response_completed",
  "event_id": "123456789",
  "object_type": "response",
  "object_id": "123456",
  "event_datetime": "2016-01-01T21:56:31.182613+00:00",
  "resources": {
    "respondent_id": "123456789",
    "recipient_id": "123456789",
    "collector_id": "123456789",
    "survey_id": "123456789",
    "user_id": "123456789"
  }
}
```

####Callback Event

Name | Description | Data Type
----- | ----- | -----
name | Webhook name | String
filter_type | Which kind of object the webhook set to filter events by: `survey` or `collector` | String-ENUM
filter_id |The id of the object triggering the event |String|
event_type | Event type that the webhook listens to: `response_completed`, `response_disqualified`, or `response_updated` | String-ENUM
event_id | Event id | String
object_type | Type of object that event occured for | String
object_id | id of object that event occured for | String
event_datetime | ISO 8601 string of date/time that the event occured | String
resources |Ids associated with th event. Depending on the webhook configuration can include: `respondent_id`, `recipient_id`, `collector_id`, `survey_id`, and `user_id`|Object



 

