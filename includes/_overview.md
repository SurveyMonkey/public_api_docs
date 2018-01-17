#Overview

##Getting Started

The SurveyMonkey API is REST-based, employs [OAuth 2.0](https://oauth.net/2/), and returns responses in [JSON](http://www.json.org/). Our documentation is organized by endpoint, has code examples in Python and cURL, and provides a Postman collection with calls for each available method.We also have a [quick start guide](#quick-start-guide-two-common-use-cases) outlining flows for some common use cases.

To use our API, you'll need to [register a draft app](#registering-an-app) to your SurveyMonkey account. You have a 90-day window to develop in a draft app, after which you'll need to [deploy](#deploying-an-app) publicly or privately. Public apps are available to anyone with a SurveyMonkey account and published in our [App Directory](https://www.surveymonkey.com/integrations/). If you're building an app for yourself or your organization, you can deploy a Private app.

###Public Apps

Public apps extend features to SurveyMonkey users. All apps must be reviewed and approved by SurveyMonkey and adhere to our [terms of use](https://developer.surveymonkey.com/tou/) before they can be published in our [App Directory](https://www.surveymonkey.com/integrations/).

Public apps use [scopes](#scopes) to request permissions from app users during OAuth. Some [scopes](#scopes) require your app's users to have a paid SurveyMonkey plan.

Public apps published in our [App Directory](https://www.surveymonkey.com/integrations/) can make unlimited requests to our API. When a Public app is in draft (during development), it's subject to [draft request limits](##request-and-response-limits).

###Private Apps

Private apps don't need to be reviewed by SurveyMonkey. Only logged-in users of the SurveyMonkey team the app is registered to can see the app in the [App Directory](https://www.surveymonkey.com/integrations/). Private apps are subject to our [terms of use](https://developer.surveymonkey.com/tou/). Private apps have [API request limits](#request-and-response-limits) and [higher limits are available for purchase](#increasing-limits).

All users of a Private app must belong to the same [SurveyMonkey team](https://help.surveymonkey.com/articles/en_US/kb/Groups) and have a [paid SurveyMonkey plan that offers direct API access](https://www.surveymonkey.com/pricing/details/?ut_source=dev_portal&amp;ut_source2=docs).

###Registering an App

Anyone with a SurveyMonkey account can register an app. Registering creates a draft app with an access token you can use to query against your account for 90 days.  No other SurveyMonkey accounts can authenticate a draft app. Before the 90-day period ends, you must deploy your app as either Public or Private and upgrade your account as needed.

###Deploying an App

Before the 90-day draft period ends, you must deploy your app or it'll be disabled. If your app is disabled, you must deploy it or contact us at [api-support@surveymonkey.com](mailto: api-support@surveymonkey.com) to request an extension.


##Scopes

Scopes allow apps to access particular resources on behalf of a user. For example, the **Create/Modify surveys** scope allows your app to create a survey in a user's account. During the OAuth process, a user is asked to grant permission to scopes your app is requesting access to.

Some scopes require your app's users to have SurveyMonkey paid plans. If your Public app uses scopes tied to paid plans, any accounts attempting to authenticate without the necessary plan will be asked to upgrade to proceed. Our request [headers](#headers) include the scopes available to users' plan, as well as those they've granted your app permission to.

You can set scopes to be required, optional, or not required in your [app's settings](https://developer.surveymonkey.com/apps/). All required scopes must be approved by and available to the user for the OAuth process to succeed.

Two scopes, **Create/Modify Responses** and **Create/Modify Surveys**, require SurveyMonkey's approval to use in a Public app. If you've deployed a Public app and want to change your scope requirements to include these, you'll need to contact us at [api-support@surveymonkey.com](mailto: api-support@surveymonkey.com) to tell us more about your app and use case.


|Scope Label|Scope Description (text shown during OAuth, "you" refers to owner of authenticating account)|Scope Name|Requires Paid SurveyMonkey Account?|
|----------|---------------------------------------|------------|---|
|View Surveys|View your surveys and those shared with you|surveys_read|No|
|Create/Modify Surveys|Create or edit surveys in your account|surveys_write|No|
|View Collectors|View collectors for your surveys and those shared with you|collectors_read|No|
|Create/Modify Collectors|Create or edit collectors for surveys in your account|collectors_write|No|
|View Contacts|View your contacts and contact lists|contacts_read|No|
|Create/Modify Contacts|Create or edit contacts in your account|contacts_write|No|
|View Responses|View if surveys in your account have responses and their metadata |responses_read|No|
|View Response Details|View answers along with responses and answer counts and trends|responses_read_detail|Yes|
|Create/Modify Responses|Create or edit survey responses in your account|responses_write|Yes|
|View Webhooks|View webhooks to receive notifications when there are changes in your account|webhooks_read|No|
|Create/Modify Webhooks|Create and edit webhooks to receive notifications when there are changes in your account|webhooks_write|No|
|View Users|View your user information|users_read|No|
|View Teams|View teams you belong to|groups_read|Yes|
|View Library Assets|View your library of survey themes and templates|library_read|No|

##Request and Response Limits

Draft and Private apps are subject to rate limits:

| Max Requests Per Minute | Max Requests Per Day
| ------- | -------
120 | 500

We permit three violations of up to 150% within a 30-day window. We begin to enforce limits at 100% once your app exceeds its limits three times within 30 days.

We return your app's rate limits, requests remaining, and seconds to reset in our request [headers](#header).

In addition, requests made to the API to create [contacts](#contacts-and-contact-lists) or send [invite messages](#collectors-and-invite-messages) are subject to our [sending and contact limits](http://help.surveymonkey.com/articles/en_US/kb/Is-there-a-limit-on-the-number-of-emails-I-can-send).

####Increasing Limits

If you think you may be in danger of frequently exceeding your request-limit threshold, please [fill out this form](https://smenterprise.surveymonkey.com/Contactsales_en?&utm_source=website&utm_medium=website&utm_content=dev_portal&utm_campaign=dev_portal&family=SME&date=2016-08-31&program=7013A000000NnGKQA0&source=dev_portal&recent=dev_portal ) with an estimate of your anticipated API activity. Additional fees may apply for increased rate limits.

####Response Limits

We also have global response limits for database utilization fair use.

Property | Limit
------- | -------
Max Page Size | 1000 resources, unless otherwise specified
Max Survey Size | 1000 questions, surveys over limit will return a 413

##Authentication

If you have a [Private app](#deploying-your-app) and will only access your own SurveyMonkey account, you can use the access token, generated when you registered your app, as part of your app's configuration. Obtain this token in the **Settings** of your app in the [**MY APPS**](https://developer.surveymonkey.com/apps/) tab.

If your app will access many SurveyMonkey accounts, implement the OAuth 2.0 three-step flow outlined below to allow users to authorize your app to access their accounts. This flow generates a long-lived access token your app can use with every API call to the associated SurveyMonkey account. It's important to note the access token only grants access when used in combination with your API credentials (client ID) and only to the SurveyMonkey account which was authorized. Your app will need to obtain additional access tokens for each SurveyMonkey account you wish to access.

If your app has required [scopes](#scopes), users will need to approve all of them and may need a [paid SurveyMonkey plan](https://www.surveymonkey.com/pricing/?ut_source=dev_portal&amp;ut_source2=docs) to successfully Oauth into your app.

###OAuth 2.0 Flow

####Step 1: Direct user to SurveyMonkey's OAuth authorization page

Your app should send the user whose SurveyMonkey account you wish to access to a specially crafted Oauth link at https://api.surveymonkey.com. The page presented to the user will identify your app, ask them to log into SurveyMonkey if they aren't already, and ask them to authorize any required [scopes](#scope).

The OAuth link should be `https://api.surveymonkey.com/oauth/authorize` with urlencoded parameters: `redirect_uri`, `client_id`, and `response_type`.

* `response_type` will always be set to the value `code`
* `client_id` the unique SurveyMonkey client id you got when registering your app
* `redirect_uri` URL encoded OAuth redirect URI you registered for your app (can be found and edited [here](https://developer.surveymonkey.com/apps/))

>Example OAuth Link

```shell
https://api.surveymonkey.com/oauth/authorize?response_type=code&redirect_uri=https%3A%2F%2Fapi.surveymonkey.com%2Fapi_console%2Foauth2callback&client_id=SurveyMonkeyApiConsole
```


```python
SM_API_BASE = "https://api.surveymonkey.com"
AUTH_CODE_ENDPOINT = "/oauth/authorize"

def oauth_dialog(client_id, redirect_uri):
	url_params = urllib.urlencode({
		"redirect_uri": redirect_uri,
		"client_id": client_id,
		"response_type": "code"
	})

	auth_dialog_uri = SM_API_BASE + AUTH_CODE_ENDPOINT + "?" + url_params
	print "\nThe OAuth dialog url was " + auth_dialog_uri + "\n"

	# Insert code here that redirects user to OAuth Dialog url
```

####Step 2: User authorization generates short-lived code

Once the user makes their choice whether to authorize access or not, SurveyMonkey will generate a 302 redirect sending their browser to your redirect URI along with a short-lived code included as a query parameter. Your app needs to use that code to make another API request before it expires (5 minutes). In that request, you'll send us the code you received, along with your client secret, client ID, and redirect URI. We'll verify all that information. If it's good, we'll return a long-lived access token in exchange.

>Generate Short Code or Deny Access

```shell
"Access Authorized" redirect: `https://api.surveymonkey.com/api_console/oauth2callback?code=SHORTLIVEDCODE`
"Access Denied" redirect: `https://api.surveymonkey.com/api_console/oauth2callback?error_description=Resource+owner+canceled+the+request&error=access_denied`
```


```python
def handle_redirect(redirect_uri):
	# Parse authorization code out of url
	query_string = urlparse.urlsplit(redirect_uri).query
	authorization_code = urlparse.parse_qs(query_string).get("code", [])

	# parse_qs returns a list for every query param, just get the first one
	if not authorization_code:
		return

	return authorization_code[0]
```

####Step 3: Exchanging for a long-lived access token

Create a form-encoded HTTP POST request to `https://api.surveymonkey.com/oauth/token` with the following encoded form fields: `client_id`, `client_secret`, `code`, `redirect_uri` and `grant_type`. The grant type must be set to "authorization_code". The `client_secret` can be found [here](https://developer.surveymonkey.com/apps/).

If successful, the access token will be returned encoded as JSON in the response body of your POST request. The key will be `access_token` and the value can be passed to our API as an HTTP header in the format `Authorization: bearer YOUR_ACCESS_TOKEN`. The value of the header must be "bearer" followed by a single space and then your access token.


>Exchange for long-lived token

```shell
curl -i -X POST https://api.surveymonkey.com/oauth/token -d \
	"client_secret=YOUR_CLIENT_SECRET \
	&code=AUTH_CODE \
	&redirect_uri=YOUR_REDIRECT_URI \
	&client_id=YOUR_CLIENT_ID \
	&grant_type=authorization_code"
```

```python
SM_API_BASE = "https://api.surveymonkey.com"
ACCESS_TOKEN_ENDPOINT = "/oauth/token"

def exchange_code_for_token(auth_code, client_secret, client_id, redirect_uri):
	data = {
		"client_secret": client_secret,
		"code": auth_code,
		"redirect_uri": redirect_uri,
		"client_id": client_id,
		"grant_type": "authorization_code"
	}

	access_token_uri = SM_API_BASE + ACCESS_TOKEN_ENDPOINT
	access_token_response = requests.post(access_token_uri, data=data)
	access_json = access_token_response.json()

	if "access_token" in access_json:
		return access_json["access_token"]
	else:
		print access_json
		return None
```

###Token expiration and revocation

Our access tokens don't currently expire but may in the future. We'll warn all developers before making changes.

Access tokens can be revoked by the user. If this happens, you'll get a JSON-encoded response body including a key `status`with a value of `1` and a key `errmsg` with the value of `Client revoked access grant` when making an API request. If you get this response, you'll need to complete OAuth again.

###Access URL

Depending on the originating datacenter of the SurveyMonkey account, the API access URL may be different than `https://api.surveymonkey.com`.

The correct API access URL for each SurveyMonkey account is returned in the response body of the [code for token exchange](#step-3-exchanging-for-a-long-lived-access-token) under the `access_url` key.


###Unauthorizing an app

To unauthorize an app:

1. Log into the linked SurveyMonkey account
2. Select **My Account** from the username dropdown in the upper right
3. Scroll to **Linked Accounts** and click **Remove** next to the app you want to unauthorize

##Quick Start Guide: Two Common Use Cases

###Export the Results of a Survey

While a call to [/surveys/{id}/responses/bulk](#surveys-id-responses-bulk) returns responses with ids for all answers chosen, your use case likely involves associating this with the values chosen. The following example takes you through exporting the results of a survey and associating responses with the corresponding answer values.

 1. Fetch the first 1,000 surveys in a SurveyMonkey account with a GET [/surveys](#surveys). This call returns a list resource containing survey ids.
 2. Using a survey id from the previous call, make a GET to [/surveys/{id}/details](#surveys-id-details). This call returns the survey's design with all question ids and answer option ids, as well as the values associated with them. Cache these values on your end to limit future calls and economize your [request and response limits](#request-and-response-limits).
 3. Using the same survey id, fetch the first 100 responses to your survey with a GET to [/surveys/{id}/respones/bulk](#surveys-id-collectors). This endpoint returns question ids and the id of the selected answer or choice for each response. You can use these to associate the selected answer id to those returned from your GET to [/surveys/{id}/details](#surveys-id-details) and match question values to the answers selected.
 4. Fetch the next page of 100 responses using the resource url returned in the `links.next` field.

To export the results of all surveys in an account, iterate through all surveys ids returned in step 1, completing steps 2 through 4.

To export the results of a single collector, a GET to /surveys/{id}/collectors returns a list collector ids associated with a given survey. A GET to [/surveys/{id}/details](#surveys-id-details) returns responses from a single collector.

###Send an Email Invitation Message

The following example takes you through creating an Email Invitation Collector and sending it to a list of recipients.

 1. Fetch the first 1,000 surveys in a SurveyMonkey account with a GET [/surveys](#surveys). This call returns a list resource containing survey ids.
 2. Using a survey id from the previous call, create a collector of type `email` by making a POST to [/surveys/{id}/collectors](#surveys-id-collectors).
 3. Create and format an email message with a POST to [/collectors/{id}/messages](#collectors-id-messages).
 4. Upload recipients to receive the message with a POST to [/collectors/{id}/messages/{id}/recipients/bulk](#collectors-id-messages-id-recipients-bulk).
 5. Send your message with a POST to [/collectors/{id}/messages/{id}/send](#collectors-id-messages-id-send).

##Pagination

When requesting list resources, you can set the size of a page by using `per_page=#` and indicate which page to return with `page=#`. So a request to `https://api.surveymonkey.com/v3/surveys?page=2&per_page=5` will return the second page of five surveys.

Any request to a list resource returns the following pagination fields, if available:

|Name|Description|Type|
|----|-----------|----|
|per_page|Number of resources per page|Integer|
|total|Number of pages available|Integer|
|page|Indicates which page is being returned|Integer|
|links.self|Resource URL for the current page|String|
|links.prev|Resource URL for the previous page of results|String|
|links.next|Resource URL for the subsequent page of results|String|
|links.first|Resource URL for the first page of results|String|
|links.last|Resource URL for the last page of results|String|

##Headers

Our API returns the following custom headers:

|Header|Description|
|------------------------|------------------|
|X-OAuth-Scopes-Available|Which [scopes](#scopes) are available to the user using an app|
|X-OAuth-Scopes-Granted|Which [scopes](#scopes) the user has granted permission to, to the app|
|X-Ratelimit-App-Global-Day-Limit|Per day request limit the app has
|X-Ratelimit-App-Global-Day-Remaining|Number of remaining requests app has before hitting daily limit
|X-Ratelimit-App-Global-Day-Reset |Number of seconds until the rate limit remaining resets
|X-Ratelimit-App-Global-Minute-Limit|Per minute request limit the app has
|X-Ratelimit-App-Global-Minute-Remaining|Number of remaining requests app has before hitting per minute limit
|X-Ratelimit-App-Global-Minute-Reset |Number of seconds until the rate limit remaining resets

##Data Types

Our API uses the following data types:

|Data Type|Description|
|------------------------|------------------|
|Integer| An integer number with a maximum value of 2147483647. Negatives are disallowed unless otherwise specified.
|String| A string of text.
|String-ENUM|Predefined string values. Values are defined per field throughout our documentation.
|Boolean| A boolean value: true or false. In JSON it will be represented using the native boolean type.
|Date string| Dates are usually in the format YYYY-MM-DDTHH:MM:SS+HH:MM. Any deviations from this are shown in the documentation. All date strings are implicitly in UTC.
|Array| A simple list of values. In JSON this will be an array.
|Object|A collection of name/value pairs. In JSON this will be an object.
|Null|A null value. In JSON this is represented as the native null type.

##Error Codes

>Example Error Response

```json
{
  "error": {
    "docs": "https://developer.surveymonkey.com/api/v3/#error-codes",
    "message": "Oh bananas! We couldn’t process your request.",
    "id": "1050",
    "name": "Internal Server Error",
    "http_status_code": 500
  }
}
```

|Error Code|HTTP Status Code|Message|
|----------|----------------|-------|
|1000|400 Bad Request|Unable to process the request with the provided input.|
|1001|400 Bad Request|The body provided was not a proper JSON string.|
|1002|400 Bad Request|Invalid schema in the body provided.
|1003|400 Bad Request|Invalid URL parameters.|
|1004|400 Bad Request|Invalid request headers.|
|1010|401 Authorization Error|The authorization token was not provided.|
|1011|401 Authorization Error|The authorization token provided was invalid.|
|1012|401 Authorization Error|The authorization token provided has expired.
|1013|401 Authorization Error|Client revoked access to the authorization token provided.|
|1014|403 Permission Error|Permission has not been granted by the user to make this request.|
|1015|403 Permission Error|The user does not have the required plan to make this request.|
|1016|403 Permission Error|The user does not have permission to access the resource.|
|1017|403 Permission Error|The user has hit a quota limit on this resource.|
|1020|404 Resource Not Found|There was an error retrieving the requested resource.|
|1025|409 Resource Conflict|Unable to complete the request due to a conflict. Check the settings for the resource.|
|1026|409 Resource Conflict|The requested resource already exists.|
|1030|413 Request Entity Too Large|The requested entity is too large, it can not be returned.|
|1040|429 Rate Limit Reached|Too many requests were made, try again later.|
|1050|500 Internal Server Error|Oh bananas! We couldn't process your request.|
|1051|503 Internal Server Error|Service unreachable. Please try again later.|
|1052|404 User Soft Deleted|The user you are making this request for has been soft deleted.|
|1053|410 User Deleted|The user you are making this request for has been deleted.|

##Help and Resources

SurveyMonkey lists code examples on [Github](https://github.com/SurveyMonkey) and monitors questions tagged as `surveymonkey` on [StackOverflow](http://stackoverflow.com/search?q=surveymonkey). If you have an SDK or example you would like added, let us know. We also offer email support at [api-support@surveymonkey.com](mailto: api-support@surveymonkey.com).

