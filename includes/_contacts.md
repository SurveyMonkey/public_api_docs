##Contacts and Contact Lists

If your application is using [email collectors](http://help.surveymonkey.com/articles/en_US/kb/Email-Invitation-Collector) to collect survey responses, these endpoints let you create contacts and contact lists to send survey invite messages to by passing a `contact_id` as an argument to `POST` [/collectors/{id}/messages/{id}/recipients](#collectors-id-messages-id-recipients). NOTE: Contacts can also be created if they are passed directly to [/collectors/{id}/messages/{id}/recipients](#collectors-id-messages-id-recipients).

###/contact_lists

>Definition

```
POST https://api.surveymonkey.net/v3/contact_lists
```

>Example Request

```shell
curl -i -X POST -H "Authorization:bearer YOUR_ACCESS_TOKEN" https://api.surveymonkey.net/v3/contact_lists?api_key=YOUR_API_KEY -d "{"name": "My Contact List"}"
```

```python
import requests

s = requests.session()
#See Requests Guide for Setting Up Requests Session

payload = {
  "name": "My Contact List"
}
url = "https://api.surveymonkey.net/v3/contact_lists?api_key=%s" % YOUR_API_KEY
s.post(url, data=payload)
```

>Example Response

```json
{
  "name": "My Contact List",
  "id": "1234",
  "href":"https://api.surveymonkey.net/v3/contact_lists/1234"
}
```

####Available Methods

 * `HEAD`: Checks if resource is available
 * `OPTIONS`: Returns available methods and options
 * `GET`: Returns all contact lists
 * `POST`: Creates a contact list, contacts can be sent survey invite messages using an email invite collector, see [Collectors and Invite Messages](#collectors-and-invite-messages)  

####Optional Query Strings for GET

Name | Description | Type
------ | ------- | -------
page | Which page of resources to return. Defaults to 1 | Integer
per_page | Number of resources to return per page | Integer

####Contact List Resource

Name | Description | Type
------ | ------- | -------
data[_].id  | Contact list id | String
data[_].name | Contact list name | String
data[_].href | Resource API URL | String

####Request Body Arguments for POST

Name | Required  |Description | Type
------ | ------- | ------- | -------
name  | No (default="New List") | Contact list name | String


###/contact_lists/{id}

>Definition

```
GET https://api.surveymonkey.net/v3/contact_lists/{contact_list_id}
```

>Example Request

```shell
curl -i -X GET -H "Authorization:bearer YOUR_ACCESS_TOKEN" https://api.surveymonkey.net/v3/contact_lists/1234?api_key=YOUR_API_KEY
```

```python
import requests

s = requests.session()

url = "https://api.surveymonkey.net/v3/contact_lists/%s?api_key=%s" % (contact_list_id, YOUR_API_KEY)
s.get(url)
```
>Example Response

```json
{
  "name": "My Contact List",
  "id": "1234",
  "href": "https://api.surveymonkey.net/v3/contact_lists/1234"
}
```
####Available Methods

 * `HEAD`: Checks if resource is available
 * `OPTIONS`: Returns available methods and options
 * `GET`: Returns a contact list 
 * `PATCH`: Modifies a contact list (updates any fields accepted as arguments to `POST` [/contact_lists](#contact_lists))
 * `PUT`: Replaces a contact list `POST` (same arguments and requirements as `POST`[/contact_lists](#contact_lists))
 * `DELETE`: Deletes a contact list

####Contact List Resource

Name | Description | Type
------ | ------- | -------
id | Contact list id | String
name | Contact list name | String


###/contact_lists/{id}/copy

>Definition

```
POST https://api.surveymonkey.net/v3/contact_lists/{contact_list_id}/copy
```

>Example Request

```shell
curl -i -X POST -H "Authorization:bearer YOUR_ACCESS_TOKEN" https://api.surveymonkey.net/v3/contact_lists/1234/copy?api_key=YOUR_API_KEY
```

```python
import requests

s = requests.session()

url = "https://api.surveymonkey.net/v3/contact_lists/%s/copy?api_key=%s" % (contact_list_id, YOUR_API_KEY)
s.post(url)
```
>Example Response

```json
{
  "name": "Copy of My Contact List",
  "id": "1234",
  "href":"https://api.surveymonkey.net/v3/contact_lists/1234"
}
```
####Available Methods

 * `POST`: Creates a copy of an existing contact list

####Contact List Resource

Name | Description | Type
------ | ------- | -------
id | Contact list id | String
name | Contact list name | String
href | Resource API URL | String


###/contact_lists/{id}/merge

>Definition

```
POST https://api.surveymonkey.net/v3/contact_lists/{contact_list_id}/merge
```

>Example Request

```shell
curl -i -X POST -H "Authorization:bearer YOUR_ACCESS_TOKEN" https://api.surveymonkey.net/v3/contact_lists/1234/merge?api_key=YOUR_API_KEY -d "{ "list_id": "4321" }"
```

```python
import requests

s = requests.session()

payload = {
  "list_id": "4321"
}
url = "https://api.surveymonkey.net/v3/contact_lists/%s/merge?api_key=%s" % (contact_list_id, YOUR_API_KEY)
s.post(url)
```

>Example Response

```json
{
  "name": "My Contact List",
  "id": "1234",
  "href":"https://api.surveymonkey.net/v3/contact_lists/1234"
}
```
####Available Methods

 * `POST`: Copies contacts in the list specified in the request body and adds to the list specified in the resource URL

####Request Body Arguments for POST

Name | Required |Description | Type
------ | ------- | ------- | -------
list_id | Yes | List id to be merged over | String

####Contact List Resource

Name | Description | Type
------ | ------- | -------
id | Contact list id | String
name | Contact list name | String
href | Resource API URL | String


###/contact_lists/{id}/contacts


>Definition

```
POST https://api.surveymonkey.net/v3/contact_lists/{contact_list_id}/contacts
```
>Example Request

```shell
curl -i -X POST -H "Authorization:bearer YOUR_ACCESS_TOKEN" https://api.surveymonkey.net/v3/contact_lists/1234/contacts?api_key=YOUR_API_KEY -d "{ "first_name": "John", "last_name": "Doe", "email": "test@surveymonkey.com"}"
```

```python
import requests

s = requests.session()

payload = {
  "first_name": "John",
  "last_name": "Doe",
  "email": "test@surveymonkey.com",
  "custom_fields": {
    "1": "Mr",
    "2": "Company",
    "3": "Address",
    "4": "City",
    "5": "Country",
    "6": "Phone Number"
  }
}
url = "https://api.surveymonkey.net/v3/contact_lists/%s/contacts?api_key=%s" % (contact_list_id, YOUR_API_KEY)
s.post(url, data=payload)
```

>Example Response

```json
{
  "id": "1234",
  "first_name": "John",
  "last_name": "Doe",
  "email": "test@surveymonkey.com",
  "custom_fields": {
    "1": "Mr",
    "2": "Company",
    "3": "Address",
    "4": "City",
    "5": "Country",
    "6": "Phone Number"
  },
  "href": "https://api.surveymonkey.net/v3/contacts/1234"
}
```
####Available Methods

 * `HEAD`: Checks if resource is available
 * `OPTIONS`: Returns available methods and options
 * `GET`: Returns all contacts in a contact list 
 * `POST`: Creates a new contact and adds them to a contact list, contacts can be sent survey invite messages using an email invite collector, see [Collectors and Invite Messages](#collectors-and-invite-messages) 

####Optional Query Strings for GET

Name | Description | Type
------ | ------- | -------
page | Which page of resources to return. Defaults to 1 | Integer
per_page | Number of resources to return per page | Integer
status | Filter by status (default=active) e.g. ['active', 'optout','bounced'] | String-ENUM
sort_by | Field used to sort returned contact list (default=email) e.g. ['email', 'first_name', 'last_name', '1', ..., '6'] | String-ENUM
sort_order | Sort order e.g. ['ASC', 'DESC'] | String-ENUM
search_by | Field used to search returned contact list e.g. ['email', 'first_name', 'last_name', '1', ..., '6'] | String-ENUM
search | Query used to search | String

####Contacts List Resource

Name | Description | Type
------ | ------- | -------
data[_].id | Contact id | String
data[\_].first_name | Contact first name | String
data[\_].last_name | Contact last name | String
data[_].email | Contact email address | String
data[_].href | Resource API URL | String

####Request Body Arguments for POST

Name | Required |Description | Type
------ | ------- | ------- | -------
first_name | Yes | Contact first name | String
last_name | Yes | Contact last name | String
email | Yes |Contact email address | String
custom_fields | No | Contact custom fields | Dictionary

###/contact_lists/{id}/contacts/bulk

>Definition

```
POST https://api.surveymonkey.net/v3/contact_lists/{contact_list_id}/contacts/bulk
```

>Example Request

```shell
curl -i -X POST -H "Authorization:bearer YOUR_ACCESS_TOKEN" https://api.surveymonkey.net/v3/contact_lists/1234/contacts/bulk?api_key=YOUR_API_KEY -d "{ "contacts": [{ "first_name": "John", "last_name": "Doe", "email": "test%40surveymonkey.com" }"
```

```python
import requests

s = requests.session()

payload = {
  "contacts": [{
    "first_name": "John",
    "last_name": "Doe",
    "email": "test@surveymonkey.com",
    "custom_fields": {
      "1": "Mr",
      "2": "Company",
      "3": "Address",
      "4": "City",
      "5": "Country",
      "6": "Phone Number"
    }
  }]
}
url = "https://api.surveymonkey.net/v3/contact_lists/%s/contacts/bulk?api_key=%s" % (contact_list_id, YOUR_API_KEY)
s.post(url, data=payload)
```

>Example Response

```json
{
  "succeeded": [{
    "first_name": "John",
    "last_name": "Doe",
    "id": "1234",
    "email": "test@surveymonkey.com",
    "custom_fields": {
      "1": "Mr",
      "2": "Company",
      "3": "Address",
      "4": "City",
      "5": "Country",
      "6": "Phone Number"
    }
  }],
  "invalids": [{
  }],
  "existing": [{
  }]
}
```
####Available Methods

 * `POST`: Creates multiple contacts and adds them to a list, contacts can be sent survey invite messages using an email invite collector, see [Collectors and Invite Messages](#collectors-and-invite-messages) 

####Request Body Arguments for POST

Name | Required | Description | Type
------ | ------- | ------- | -------
data[\_].first_name | Yes | Contact first name | String
data[\_].last_name | Yes | Contact last name | String
data[_].email | Yes | Contact email | String
data[\_].custom_fields | No | Custom contact fields | Dictionary


###/contacts

>Definition

```
POST https://api.surveymonkey.net/v3/contacts
```

>Example Request

```shell
curl -i -X POST -H "Authorization:bearer YOUR_ACCESS_TOKEN" https://api.surveymonkey.net/v3/contacts?api_key=YOUR_API_KEY -d "{ "first_name": "John", "last_name": "Doe", "email": "test%40surveymonkey.com" }"
```

```python
import requests

s = requests.session()

payload = {
  "first_name": "John",
  "last_name": "Doe",
  "email": "test@surveymonkey.com",
  "custom_fields": {
    "1": "Mr",
    "2": "Company",
    "3": "Address",
    "4": "City",
    "5": "Country",
    "6": "Phone Number"
  }
}
url = "https://api.surveymonkey.net/v3/contacts?api_key=%s" % YOUR_API_KEY
s.post(url, data=payload)
```

>Example Response

```json
{
  "id": "1234",
  "first_name": "John",
  "last_name": "Doe",
  "email": "test@surveymonkey.com",
  "custom_fields": {
    "1": "Mr",
    "2": "Company",
    "3": "Address",
    "4": "City",
    "5": "Country",
    "6": "Phone Number"
  },
  "href": "https://api.surveymonkey.net/v3/contacts/1234"
}
```

####Available Methods

 * `HEAD`: Checks if resource is available
 * `OPTIONS`: Returns available methods and options
 * `GET`: Returns a list of all contacts
 * `POST`: Creates a new contact, contacts can be sent survey invite messages using an email invite collector, see [Collectors and Invite Messages](#collectors-and-invite-messages) 

####Optional Query Strings for GET

Name | Description | Type
------ | ------- | -------
page | Page number. Defaults to 1 | Integer
per_page | Number of contacts to return per page | Integer
status | Filter by status (default=active): 'active', 'optout', or 'bounced'] | String-ENUM
sort_by | Field used to sort returned contact list (default=email) e.g. ['email', 'first_name', 'last_name', '1', ..., '6'] | String-ENUM
sort_order | Sort order: 'ASC' or 'DESC' | String-ENUM
search_by | Field used to search returned contact list e.g. ['email', 'first_name', 'last_name', '1', ..., '6'] | String-ENUM
search | Query used to search | String

####Contacts List Resource

Name |Description | Type
------ | ------- | -------
data[_].id | Contact id | String
data[\_].first_name | Contact first name | String
data[\_].last_name | Contact last name | String
data[_].email | Contact email address | String
data[_].href | Resource API URL | String

####Request Body Arguments for POST

Name | Required | Description | Type
------ | ------- | ------- | -------
first_name | Yes | Contact first name | String
last_name | Yes | Contact last name | String
email | Yes | Contact email address | String
custom_fields | No | Contact custom field | Dictionary

###/contacts/bulk

>Definition

```
POST https://api.surveymonkey.net/v3/contacts/bulk
```

>Example Request

```shell
curl -i -X POST -H "Authorization:bearer YOUR_ACCESS_TOKEN" https://api.surveymonkey.net/v3/contacts?api_key=YOUR_API_KEY -d "{ "contacts": [{ "first_name": "John", "last_name": "Doe", "email": "test%40surveymonkey.com" }"
```

```python
import requests

s = requests.session()

payload = {
  "contacts": [{
    "first_name": "John",
    "last_name": "Doe",
    "email": "test@surveymonkey.com",
    "custom_fields": {
      "1": "Mr",
      "2": "Company",
      "3": "Address",
      "4": "City",
      "5": "Country",
      "6": "Phone Number"
    }
  }]
}
url = "https://api.surveymonkey.net/v3/contacts/bulk?api_key=%s" % YOUR_API_KEY
s.post(url, data=payload)
```

>Example Response

```json
{
  "succeeded": [{
    "first_name": "John",
    "last_name": "Doe",
    "id": "1234",
    "email": "test@surveymonkey.com",
    "custom_fields": {
      "1": "Mr",
      "2": "Company",
      "3": "Address",
      "4": "City",
      "5": "Country",
      "6": "Phone Number"
    }
  }],
  "invalids": [{
  }],
  "existing": [{
  }]
}
```
####Available Methods

 * `POST`: Creates multiple contacts, contacts can be sent survey invite messages using an email invite collector, see [Collectors and Invite Messages](#collectors-and-invite-messages) 

####Request Body Arguments for POST

Name | Required | Description | Type
------ | ------- | ------- | -------
data[\_].first_name | Yes | Contact first name | String
data[\_].last_name | Yes | Contact last name | String
data[_].email | Yes | Contact email | String
data[\_].custom_fields | No | Custom contact fields | Dictionary


###/contacts/{id}

>Definition

```
GET https://api.surveymonkey.net/v3/contacts/{contact_id}
```

>Example Request

```shell
curl -i -X GET -H "Authorization:bearer YOUR_ACCESS_TOKEN" https://api.surveymonkey.net/v3/contacts/1234?api_key=YOUR_API_KEY
```

```python
import requests

s = requests.session()

url = "https://api.surveymonkey.net/v3/contacts/%s?api_key=%s" % (contact_id, YOUR_API_KEY)
s.get(url)
```
>Example Response

```json
{
  "id": "1234",
  "first_name": "John",
  "last_name": "Doe",
  "email": "test@surveymonkey.com",
  "custom_fields": {
    "1": "Mr",
    "2": "Company",
    "3": "Address",
    "4": "City",
    "5": "Country",
    "6": "Phone Number"
  }
}
```
####Available Methods

 * `HEAD`: Checks if resource is available
 * `OPTIONS`: Returns available methods and options
 * `GET`: Returns a contact
 * `PATCH`: Modifies a contact (updates any fields accepted as arguments to `POST` [/contacts](#contacts)
 * `PUT`: Replaces a contact (same arguments and requirements as `POST`[/contacts](#contacts))
 * `DELETE`: Deletes a contact


####Contact Resource

Name | Description | Type
------ | ------- | -------
id | Contact id | String
first_name | Contact first name | String
last_name | Contact last name | String
email | Contact email address | String
custom_fields | Contact custom fields | Dictionary


###/contact_fields

>Definition

```
GET https://api.surveymonkey.net/v3/contact_fields
```

>Example Request

```shell
curl -i -X GET -H "Authorization:bearer YOUR_ACCESS_TOKEN" https://api.surveymonkey.net/v3/contact_fields?api_key=YOUR_API_KEY
```

```python
import requests

s = requests.session()

url = "https://api.surveymonkey.net/v3/contact_fields?api_key=%s" % YOUR_API_KEY
s.get(url)
```

>Example Response

```json
{
  "page": 1,
  "per_page": 1,
  "total": 1,
  "data": [
    {
      "href": "https://api.surveymonkey.net/v3/contact_fields/1",
      "id": "1",
      "label": "Custom 1"
    }]
}
```

####Available Methods

 * `HEAD`: Checks if resource is available
 * `OPTIONS`: Returns available methods and options
 * `GET`: Returns a list of all [custom contacts fields](http://help.surveymonkey.com/articles/en_US/kb/Custom-Data)

####Optional Query Strings for GET

Name | Description | Type
------ | ------- | -------
page | Page number. Defaults to 1 | Integer
per_page | Number of contacts to return per page | Integer

####Contacts List Resource

Name |Description | Type
------ | ------- | -------
data[_].id | Contact id | String
data[_].label | Contact Field Label | String
data[_].href | Resource API URL | String


###/contact_fields/{id}

>Definition

```
PATCH https://api.surveymonkey.net/v3/contact_fields/{contact_field_id}
```

>Example Request

```shell
curl -i -X PATCH -H "Authorization:bearer YOUR_ACCESS_TOKEN" https://api.surveymonkey.net/v3/contact_fields/1?api_key=YOUR_API_KEY -d "{"label: "5"}"
```

```python
import requests

s = requests.session()

payload = {
  "label" = "address"
}
url = "https://api.surveymonkey.net/v3/contact_fields/1?api_key=%s" % YOUR_API_KEY
s.patch(url)
```
>Example Response

```json
{
  "href": "https://api.surveymonkey.net/v3/contact_fields/1",
  "id": "1",
  "label": "address"
}
```
####Available Methods

 * `HEAD`: Checks if resource is available
 * `OPTIONS`: Returns available methods and options
 * `GET`: Returns the specified [custom contact field](http://help.surveymonkey.com/articles/en_US/kb/Custom-Data)
 * `PATCH`: Modifies a [custom contact field's](http://help.surveymonkey.com/articles/en_US/kb/Custom-Data) label

####Request Body Arguments for PATCH

Name | Required | Description | Type
------ | ------- | ------- | -------
label | Yes | Label assigned to the custom contact feild | String


####Contact Field Resource

Name | Description | Type
------ | ------- | -------
id | Contact Field id | String
label | Contact Field Label | String

