#Overview

##Getting Started

The SurveyMonkey API is REST-based, uses OAuth2 for authentication, and returns responses in JSON. To get started you will [register an app](#registering-an-app) in our developer portal. Before you register, you should determine if your app will eventually be [deployed](#deploying-an-app) as Public or Private and which [scopes](#scopes) you will need.

All Public apps need to be approved by SurveyMonkey before they can be deployed, use of certain scopes will also need to be approved. Read more about [scopes](#scopes) and [deploying your app](#deploying-your-app) to determine if you should contact us before you begin to develop your app.

Newly registered apps are given a draft state window in which developers can use all paid scopes for free when querying against the associated SurveyMonkey account for up to 90 days. No other SurveyMonkey accounts can authenticate a draft app. Before the 90-day period ends, you must deploy your app as either Public or Private and upgrade your account as needed.

SurveyMonkey lists code examples on [Github](https://github.com/SurveyMonkey) and monitors questions tagged as `surveymonkey` on [StackOverflow](http://stackoverflow.com/search?q=surveymonkey). If you have an SDK or example you would like added, let us know. We also offer email support at [api-support@surveymonkey.com](mailto: api-support@surveymonkey.com).

###Registering an App

When registering your app it is important to know if you will eventually deploy as a Private or Public app and, for Public apps, which scopes you plan to use as these determine if users need a pro SurveyMonkey plan to use your app. SurveyMonkey reviews all Public apps before they can be deployed. Read more about [scopes](#scopes) and [deploying your app](#deploying-your-app) before you register an app.

To register an app:

1. Click on the **MY APPS** tab in the upper left corner and sign into your SurveyMonkey account.
1. Click **+ Add New App**. Enter your **App Name** and click **Create App**. Under **App Details** you'll find your client id to use for OAuth, as well as an access token for your own SurveyMonkey account. New apps are given a 90 day draft state during which you can use paid scopes for free.
1. Click **Settings** to edit your app's **Redirect URI**, and review and adjust scopes for your app. Scopes allow your application to access particular resources on behalf of a user. For Public apps, the scopes you use determine which paid SurveyMonkey plan your app's users will need and if your application will need to be approved by SurveyMonkey before you can deploy. Click on scopes to toggle their requirements and click **Update Scopes** when finished.

###Deploying an App

When you create a new app you are given a 90-day draft window during which you can use all paid [scopes](#scopes) for free when querying against the associated SurveyMonkey account. No other SurveyMonkey accounts can authenticate a draft app.

Before the 90-day period ends, you must deploy your app as either Public or Private or your app will be disabled. If your app is disabled, you can deploy it as either Public or Private, or contact us at [api-support@surveymonkey.com](mailto: api-support@surveymonkey.com) to request an extension.

To deploy your app:

 1. Visit your app's settings in the [developer portal](https://developer.surveymonkey.com/apps/) and select either **Public** or **Private**. See below for details on these options.
 2. If necessary, [upgrade](https://www.surveymonkey.com/pricing/?ut_source=dev_portal&amp;ut_source2=docs) your account to the required plan. This will be Platinum for any Private apps and will vary for Public ones based on the scopes you use.

####Public Apps

All public apps will need to be approved by SurveyMonkey to be deployed, please contact us at [api-support@surveymonkey.com](mailto: api-support@surveymonkey.com) to tell us more about your app and use case.

Deploy as a Public app only if:

 * your app will be used by many SurveyMonkey accounts that do not belong to the same group plan.

Examples of Public apps include:

 * An integration of SurveyMonkey functionality into a pre-existing tool
 * Stand alone applications that extend SurveyMonkey's functionality

The [scopes](#scopes) that your app uses determine the SurveyMonkey plan level users will need to access it.

####Private Apps

Deploying as a Private app requires you to [upgrade](https://www.surveymonkey.com/pricing/?ut_source=dev_portal&amp;ut_source2=docs) to a Platinum or Platinum group plan. Private apps can use all available scopes. Private apps are subject to [request limits](#request-and-response-limits).

Deploy as a Private app if:

 * your app will only be used by one SurveyMonkey account or many SurveyMonkey accounts that belong to the same [Platinum group plan](http://help.surveymonkey.com/articles/en_US/kb/Groups)

 Examples of Private apps include:

 * A developer uses the API to send surveys or import survey results data from their own account
 * A developer purchases SurveyMonkey seats on behalf of employees or customers and builds an application for multiple users


###Scopes

Scopes allow Public apps to access particular resources on behalf of a user. For example, the **Create/Modify surveys** scope allows your app to create a survey in a user's account. During the OAuth process the user will approve or disapprove the scopes you have requested access to. Based on your app's needs you can choose to either require scopes, set them as optional, or not require them. All required scopes must be approved by the user for the OAuth process to succeed.

Some scopes are only available to accounts on SurveyMonkey paid plans. If your Public application uses scopes tied to paid plans, any accounts authenticating with your application need that plan or higher. We return scopes available to users as well as those a user has granted to your app in our request [headers](#headers).

Two scopes **Create/Modify Responses** and **Create/Modify Surveys** require SurveyMonkey's approval to use in a Public app. If you've deployed a Public app and want to change your scope requirements to include these, you'll need to contact us at [api-support@surveymonkey.com](mailto: api-support@surveymonkey.com) to tell us more about your app and use case.


|Scope Name|Scope Description (text used for OAuth, "you" refers to owner of authenticating account)|Plan Needed|
|----------|---------------------------------------|-----------|
|View Surveys|View your surveys and those shared with you|BASIC (Free)|
|Create/Modify Surveys|Create or edit surveys in your account|Any Paid Plan|
|View Collectors|View collectors for your surveys and those shared with you|BASIC (Free)|
|Create/Modify Collectors|Create or edit collectors for surveys in your account|BASIC (Free)|
|View Contacts|View your contacts and contact lists|BASIC (Free)|
|Create/Modify Contacts|Create or edit contacts in your account|BASIC (Free)|
|View Responses|View if surveys in your account have responses and their metadata |BASIC (Free)|
|View Response Details|View answers along with responses and answer counts and trends|Any Annual Plan|
|Create/Modify Responses|Create or edit survey responses in your account|PLATINUM/ENTERPRISE|
|View Webhooks|View webhooks to receive notifications when there are changes in your account|BASIC (Free)|
|Create/Modify Webhooks|Create and edit webhooks to receive notifications when there are changes in your account|BASIC (Free)|
|View Users|View your user information|BASIC (Free)|
|View Groups|View groups you belong to|GOLD|
|View Library Assets|View your library of survey themes and templates|BASIC (Free)|

##Request and Response Limits

Draft and Private apps are subject to the following API Rate limits:

| Max Requests Per Minute | Max Requests Per Day
| ------- | -------
120 | 500

We return your app's rate limits, requests remaining, and seconds to reset in our request [headers](#header).

In addition, requests made to the API to create [contacts](#contacts-and-contact-lists) or send [invite messages](#collectors-and-invite-messages), are subject to our [sending and contact limits](http://help.surveymonkey.com/articles/en_US/kb/Is-there-a-limit-on-the-number-of-emails-I-can-send).

####Increasing Limits

If you think you may be in danger of exceeding your request-limit threshold, please [fill out this form](https://smenterprise.surveymonkey.com/Contactsales_en?&utm_source=website&utm_medium=website&utm_content=dev_portal&utm_campaign=dev_portal&family=SME&date=2016-08-31&program=7013A000000NnGKQA0&source=dev_portal&recent=dev_portal ) with an estimate of your anticipated API activity. SurveyMonkey will review all requests within 5 business days. Additional fees may apply for increased rate limits.

####Response Limits

We also have global response limits for database utilization fair use.

Property | Limit
------- | -------
Max Page Size | 1000 unless otherwise specified
Max Survey Size | 1000 questions, surveys over limit will return a 413

##Authentication

<aside class="notice">We've updated our authentication and are no longer using Mashery. We now generate a unique client id that is not your Mashery username, and have removed the use of API keys. If you are registering a new app or refreshing your credentials you should follow the <a href="https://developer.surveymonkey.com/api/v3/#new-authentication">NEW Authentication flow</a>. If you created your app before Nov 1st, 2016, your existing credentials will continue to work as outlined in the <a href="https://developer.surveymonkey.com/api/v3/#old-authentication">OLD Authentication</a> as long as you don't refresh them in our developer portal.</aside>

The SurveyMonkey API supports OAuth 2.0.

If you have a [Private application](#deploying-your-app) and will only access your own SurveyMonkey account, you can use the access token, generated when you registered your app, as part of your application's configuration. Obtain this token in the **Settings** of your app in the [**MY APPS**](https://developer.surveymonkey.com/apps/) tab.

If your application will access many SurveyMonkey accounts, implement the OAuth 2.0 three-step flow outlined below to allow users to authorize your app to access their accounts. This flow generates a long-lived access token your application can use with every API call to the associated SurveyMonkey account. It's important to note that the access token only grants access when used in combination with your API credentials (client ID) and only to the SurveyMonkey account which was authorized. Your application will need to obtain additional access tokens for each SurveyMonkey account you wish to access.

If your [Public application](#deploying-your-app) has required [scopes](#scopes), users may need a [paid SurveyMonkey plan](https://www.surveymonkey.com/pricing/?ut_source=dev_portal&amp;ut_source2=docs) to successfully Oauth into your application.

###NEW Authentication

####Step 1: Direct user to SurveyMonkey's OAuth authorization page

You applications should send the user whose SurveyMonkey account you wish to access to a specially crafted Oauth link at https://api.surveymonkey.net. The page presented to the user there will identify the application name you configured when you registered your application. Users will either be asked to enter their SurveyMonkey user name and password, or, if they are already logged into SurveyMonkey, just an "Authorize" button.

The OAuth link should be `https://api.surveymonkey.net/oauth/authorize` with urlencoded parameters: `redirect_uri`, `client_id`, and `response_type`.

* `response_type` will always be set to the value `code`
* `client_id` the unique SurveyMonkey client id you got when registering your app
* `redirect_uri` URL encoded OAuth redirect URI you registered for your application (can be found and edited [here](https://developer.surveymonkey.com/apps/))

>Example OAuth Link

```shell
https://api.surveymonkey.net/oauth/authorize?response_type=code&redirect_uri=https%3A%2F%2Fapi.surveymonkey.com%2Fapi_console%2Foauth2callback&client_id=SurveyMonkeyApiConsole
```


```python
SM_API_BASE = "https://api.surveymonkey.net"
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

####Step 2: User authorization generates short lived code

Once the user makes their choice whether to authorize access or not, SurveyMonkey will generate a 302 redirect sending their browser to your redirect URI along with a short-lived code included as a query parameter. Your application needs to use that code to make another API request before it expires (5 minutes). In that request, you will send us the code you received along with your client secret, client ID, and redirect URI. We will verify all that information. If it's good, we will return a long-lived access token in exchange.

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

Create a form-encoded HTTP POST request to `https://api.surveymonkey.net/oauth/token` with the following encoded form fields: `client_id`, `client_secret`, `code`, `redirect_uri` and `grant_type`. The grant type must be set to "authorization_code". The `client_secret` can be found [here](https://developer.surveymonkey.com/apps/).

If successful, the access token will be returned encoded as JSON in the response body of your POST request. The key will be `access_token` and the value can be passed to our API as an HTTP header in the format `Authorization: bearer YOUR_ACCESS_TOKEN`. The value of the header must be "bearer" followed by a single space and then your access token.


>Exchange for long-lived token

```shell
curl -i -X POST https://api.surveymonkey.net/oauth/token -d \
	"client_secret=YOUR_CLIENT_SECRET \
	&code=AUTH_CODE \
	&redirect_uri=YOUR_REDIRECT_URI \
	&client_id=YOUR_CLIENT_ID \
	&grant_type=authorization_code"
```

```python
SM_API_BASE = "https://api.surveymonkey.net"
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

###OLD Authentication

<aside class="notice">We've updated our authentication flow and are no longer using Mashery.  If you are <a href="https://developer.surveymonkey.com/apps/">registering a new app</a> or refreshing credentials for an existing app you should follow the <a href="https://developer.surveymonkey.com/api/v3/#new-authentication">NEW Authentication flow</a>. Existing authentication credentials will continue to work.</aside>

All code examples in our documentation assume use of our [NEW Authentication](#NEW-Authentication). If you're using our OLD Authentication, you'll need to pass your API key with each call like so:

`curl -i -X GET -H "Authorization:bearer YOUR_ACCESS_TOKEN" -H "Content-Type": "application/json" https://api.surveymonkey.net/v3/users/me?api_key=YOUR_API_KEY`

####Step 1: Direct user to SurveyMonkey's OAuth authorization page

You applications should send the user whose SurveyMonkey account you wish to access to a specially crafted Oauth link at https://api.surveymonkey.net. The page presented to the user there will identify the application name you configured when you registered your application. Users will either be asked to enter their SurveyMonkey user name and password, or, if they are already logged into SurveyMonkey, just an "Authorize" button.

The OAuth link should be `https://api.surveymonkey.net/oauth/authorize` with urlencoded parameters: `redirect_uri`, `client_id`, `response_type`, and `api_key`.

* `response_type` will always be set to the value `code`
* `client_id` your Mashery user name
* `redirect_uri` URL encoded OAuth redirect URI you registered for your application (can be found and edited [here](https://developer.surveymonkey.com/apps/))

>Example OAuth Link

```shell
https://api.surveymonkey.net/oauth/authorize?response_type=code&redirect_uri=https%3A%2F%2Fapi.surveymonkey.com%2Fapi_console%2Foauth2callback&client_id=SurveyMonkeyApiConsole&api_key=u366xz3zv6s9jje5mm3495fk
```


```python
SM_API_BASE = "https://api.surveymonkey.net"
AUTH_CODE_ENDPOINT = "/oauth/authorize"

def oauth_dialog(client_id, redirect_uri, api_key):
	url_params = urllib.urlencode({
		"redirect_uri": redirect_uri,
		"client_id": client_id,
		"response_type": "code",
		"api_key": api_key
	})

	auth_dialog_uri = SM_API_BASE + AUTH_CODE_ENDPOINT + "?"" + url_params
	print "\nThe OAuth dialog url was " + auth_dialog_uri + "\n"

	# Insert code here that redirects user to OAuth Dialog url
```

####Step 2: User authorization generates short lived code

Once the user makes their choice whether to authorize access or not, SurveyMonkey will generate a 302 redirect sending their browser to your redirect URI along with a short-lived code included as a query parameter. Your application needs to use that code to make another API request before it expires (5 minutes). In that request, you will send us the code you received along with your client secret, client ID, API key, and redirect URI. We will verify all that information. If it's good, we will return a long-lived access token in exchange.

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

Create a form-encoded HTTP POST request to `https://api.surveymonkey.net/oauth/token?api_key=YOUR_API_KEY` with the following encoded form fields: `client_secret`, `code`, `redirect_uri` and `grant_type`. The grant type must be set to "authorization_code". The `client_secret` and `api_key` can be found [here](https://developer.surveymonkey.com/apps/).

If successful, the access token will be returned encoded as JSON in the response body of your POST request. The key will be `access_token` and the value can be passed to our API as an HTTP header in the format `Authorization: bearer YOUR_ACCESS_TOKEN`. The value of the header must be "bearer" followed by a single space and then your access token.


>Exchange for long-lived token

```shell
curl -i -X POST https://api.surveymonkey.net/oauth/token?api_key=YOUR_API_KEY -d \
	"client_secret=YOUR_CLIENT_SECRET \
	&code=AUTH_CODE \
	&redirect_uri=YOUR_REDIRECT_URI \
	&client_id=YOUR_CLIENT_ID \
	&grant_type=authorization_code"
```

```python
SM_API_BASE = "https://api.surveymonkey.net"
ACCESS_TOKEN_ENDPOINT = "/oauth/token"

def exchange_code_for_token(auth_code, api_key, client_secret, client_id, redirect_uri):
	data = {
		"client_secret": client_secret,
		"code": auth_code,
		"redirect_uri": redirect_uri,
		"client_id": client_id,
		"grant_type": "authorization_code"
	}

	access_token_uri = SM_API_BASE + ACCESS_TOKEN_ENDPOINT + "?api_key=" + api_key
	access_token_response = requests.post(access_token_uri, data=data)
	access_json = access_token_response.json()

	if "access_token" in access_json:
		return access_json["access_token"]
	else:
		print access_json
		return None
```

###Token expiration and revocation

Our access tokens do not currently expire but may in the future. We will warn all developers before making changes.

Access tokens can be revoked by the user. If this happens, you will get a JSON-encoded response body including a key `status`with a value of `1` and a key `errmsg` with the value of `Client revoked access grant` when making an API request. If you get this response, you will need to complete OAuth again.

###Unauthorizing an app

To unauthorize an app:

1. Log into the linked SurveyMonkey account
2. Select **My Account** from the username dropdown in the upper right
3. Scroll to **Linked Accounts** and click **Remove** next to the app you want to unauthorize

##Pagination

When requesting list resources, you can set the size of a page by using `per_page=#` and indicate which page to return with `page=#`. So a request to `https://api.surveymonkey.net/v3/surveys?page=2&per_page=5` will return the second page of five surveys.

Any request to a list resource returns the following pagination fields, if available:

|Name|Description|Type|
|----|-----------|----|
|per_page|Indicates the number of resources per page.|Integer|
|total|Indicates the number of pages available.|Integer|
|page|Indicates which page is being returned.|Integer|
|links.self|Resource URL for the current page.|String|
|links.prev|Resource URL for the previous page of results.|String|
|links.next|Resource URL for the subsequent page of results.|String|
|links.first|Resource URL for the first page of results.|String|
|links.last|Resource URL for the last page of results.|String|

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

Our API uses the following data types.

|Data Type|Description|
|------------------------|------------------|
|Integer| An integer number with a maximum value of 2147483647. Negatives are disallowed unless otherwise specified.
|String| A string of text.
|String-ENUM|Predifined string values. Values are defined per field throughout our documnentation.
|Boolean| A boolean value: true or false. In JSON it will be represented using the native boolean type.
|Date string| Dates are usually in the format YYYY-MM-DDTHH:MM:SS+HH:MM. Any deviations from this are shown in the documenation. All date strings are implicitly in UTC.
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

