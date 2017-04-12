##Contacts and Contact Lists

If your application is using [email collectors](http://help.surveymonkey.com/articles/en_US/kb/Email-Invitation-Collector) to collect survey responses, these endpoints let you create contacts and contact lists to send survey invite messages to by passing a `contact_id` as an argument to `POST` [/collectors/{id}/messages/{id}/recipients](#collectors-id-messages-id-recipients). NOTE: Contacts can also be created if they are passed directly to [/collectors/{id}/messages/{id}/recipients](#collectors-id-messages-id-recipients).

###/contact_lists

>Definition

```
POST https://api.surveymonkey.net/v3/contact_lists
```

>Example Request

```shell
curl -i -X POST -H "Authorization:bearer YOUR_ACCESS_TOKEN" -H "Content-Type": "application/json" https://api.surveymonkey.net/v3/contact_lists -d "{"name": "My Contact List"}"
```

```python
import requests

s = requests.session()
s.headers.update({
  "Authorization": "Bearer %s" % YOUR_ACCESS_TOKEN,
  "Content-Type": "application/json"
})

payload = {
  "name": "My Contact List"
}
url = "https://api.surveymonkey.net/v3/contact_lists"
s.post(url, json=payload)
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
 * `GET`: Returns all contact lists. Public App users need access to the **View Contacts** [scope](#scopes)
 * `POST`: Creates a contact list, contacts can be sent survey invite messages using an email invite collector, see [Collectors and Invite Messages](#collectors-and-invite-messages). Public App users need access to the **Create/Modify Contacts** [scope](#scopes) 

####Optional Query Strings for GET

Name | Description | Data Type
------ | ------- | -------
page | Which page of resources to return. Defaults to 1 | Integer
per_page | Number of resources to return per page | Integer

####Contact List Resource

Name | Description | Data Type
------ | ------- | -------
data[\_].id  | Contact list id | String
data[\_].name | Contact list name | String
data[\_].href | Resource API URL | String

####Request Body Arguments for POST

Name | Required  |Description | Data Type
------ | ------- | ------- | -------
name  | No (default="New List") | Contact list name | String


###/contact_lists/{id}

>Definition

```
GET https://api.surveymonkey.net/v3/contact_lists/{contact_list_id}
```

>Example Request

```shell
curl -i -X GET -H "Authorization:bearer YOUR_ACCESS_TOKEN" -H "Content-Type": "application/json" https://api.surveymonkey.net/v3/contact_lists/1234
```

```python
import requests

s = requests.session()
s.headers.update({
  "Authorization": "Bearer %s" % YOUR_ACCESS_TOKEN,
  "Content-Type": "application/json"
})

url = "https://api.surveymonkey.net/v3/contact_lists/%s" % (contact_list_id)
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
 * `GET`: Returns a contact list. Public App users need access to the **View Contacts** [scope](#scopes) 
 * `PATCH`: Modifies a contact list (updates any fields accepted as arguments to `POST` [/contact_lists](#contact_lists)). Public App users need access to the **Create/Modify Contacts** [scope](#scopes)
 * `PUT`: Replaces a contact list `POST` (same arguments and requirements as `POST`[/contact_lists](#contact_lists)). Public App users need access to the **Create/Modify Contacts** [scope](#scopes)
 * `DELETE`: Deletes a contact list. Public App users need access to the **Create/Modify Contacts** [scope](#scopes)

####Contact List Resource

Name | Description | Data Type
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
curl -i -X POST -H "Authorization:bearer YOUR_ACCESS_TOKEN" -H "Content-Type": "application/json" https://api.surveymonkey.net/v3/contact_lists/1234/copy
```

```python
import requests

s = requests.session()
s.headers.update({
  "Authorization": "Bearer %s" % YOUR_ACCESS_TOKEN,
  "Content-Type": "application/json"
})

url = "https://api.surveymonkey.net/v3/contact_lists/%s/copy" % (contact_list_id)
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

 * `POST`: Creates a copy of an existing contact list. Requires **Create/Modify Contacts** [scope](#scopes)

####Contact List Resource

Name | Description | Data Type
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
curl -i -X POST -H "Authorization:bearer YOUR_ACCESS_TOKEN" -H "Content-Type": "application/json" https://api.surveymonkey.net/v3/contact_lists/1234/merge-d "{ "list_id": "4321" }"
```

```python
import requests

s = requests.session()
s.headers.update({
  "Authorization": "Bearer %s" % YOUR_ACCESS_TOKEN,
  "Content-Type": "application/json"
})

payload = {
  "list_id": "4321"
}
url = "https://api.surveymonkey.net/v3/contact_lists/%s/merge" % (contact_list_id)
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

 * `POST`: Copies contacts in the list specified in the request body and adds to the list specified in the resource URL. Public App users need access to the **Create/Modify Contacts** [scope](#scopes)

####Request Body Arguments for POST

Name | Required |Description | Data Type
------ | ------- | ------- | -------
list_id | Yes | List id to be merged over | String

####Contact List Resource

Name | Description | Data Type
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
curl -i -X POST -H "Authorization:bearer YOUR_ACCESS_TOKEN" -H "Content-Type": "application/json" https://api.surveymonkey.net/v3/contact_lists/1234/contacts -d "{ "first_name": "John", "last_name": "Doe", "email": "test@surveymonkey.com"}"
```

```python
import requests

s = requests.session()
s.headers.update({
  "Authorization": "Bearer %s" % YOUR_ACCESS_TOKEN,
  "Content-Type": "application/json"
})

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
url = "https://api.surveymonkey.net/v3/contact_lists/%s/contacts" % (contact_list_id)
s.post(url, json=payload)
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
 * `GET`: Returns all contacts in a contact list. Public App users need access to the **View Contacts** [scope](#scopes)
 * `POST`: Creates a new contact and adds them to a contact list, contacts can be sent survey invite messages using an email invite collector, see [Collectors and Invite Messages](#collectors-and-invite-messages). Public App users need access to the **Create/Modify Contacts** [scope](#scopes) 

####Optional Query Strings for GET

Name | Description | Data Type
------ | ------- | -------
page | Which page of resources to return. Defaults to 1 | Integer
per_page | Number of resources to return per page | Integer
status | Filter by status (default=active): `active`, `optout`, `bounced` | String-ENUM
sort_by | Field used to sort returned contact list (default=email): `email`, `first_name`, `last_name`, `1`, ..., `6` | String-ENUM
sort_order | Sort order e.g. ['ASC', 'DESC'] | String-ENUM
search_by | Field used to search returned contact list: : `email`, `first_name`, `last_name`, `1`, ..., `6`  | String-ENUM
search | Query used to search | String

####Contacts List Resource

Name | Description | Data Type
------ | ------- | -------
data[\_].id | Contact id | String
data[\_].first_name | Contact first name | String
data[\_].last_name | Contact last name | String
data[\_].email | Contact email address | String
data[\_].href | Resource API URL | String

####Request Body Arguments for POST

Name | Required |Description | Data Type
------ | ------- | ------- | -------
first_name | Yes | Contact first name | String
last_name | Yes | Contact last name | String
email | Yes |Contact email address | String
custom_fields | No | Contact custom fields | Object 

###/contact_lists/{id}/contacts/bulk

>Definition

```
POST https://api.surveymonkey.net/v3/contact_lists/{contact_list_id}/contacts/bulk
```

>Example Request

```shell
curl -i -X POST -H "Authorization:bearer YOUR_ACCESS_TOKEN" -H "Content-Type": "application/json" https://api.surveymonkey.net/v3/contact_lists/1234/contacts/bulk -d "{ "contacts": [{ "first_name": "John", "last_name": "Doe", "email": "test%40surveymonkey.com" }"
```

```python
import requests

s = requests.session()
s.headers.update({
  "Authorization": "Bearer %s" % YOUR_ACCESS_TOKEN,
  "Content-Type": "application/json"
})

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
url = "https://api.surveymonkey.net/v3/contact_lists/%s/contacts/bulk" % (contact_list_id)
s.post(url, json=payload)
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

 * `GET`: Returns a list of all contacts in the list with all available fields. Public App users need access to the **View Contacts** [scope](#scopes)
 * `POST`: Creates multiple contacts and adds them to a list, contacts can be sent survey invite messages using an email invite collector, see [Collectors and Invite Messages](#collectors-and-invite-messages). Public App users need access to the **Create/Modify Contacts** [scope](#scopes)

####Contacts List Resource

Name | Description |  Data Type
------ | ------- | -------
data[\_].id | Contact id | String
data[\_].first_name | Contact first name | String
data[\_].last_name | Contact last name | String
data[\_].email | Contact email address | String
data[\_].custom_fields | Contact custom fields | Object
data[\_].href | Resource API URL | String

####Request Body Arguments for POST

Name | Required | Description | Data Type
------ | ------- | ------- | -------
data[\_].first_name | Yes | Contact first name | String
data[\_].last_name | Yes | Contact last name | String
data[\_].email | Yes | Contact email | String
data[\_].custom_fields | No | Custom contact fields | Object


###/contacts

>Definition

```
POST https://api.surveymonkey.net/v3/contacts
```

>Example Request

```shell
curl -i -X POST -H "Authorization:bearer YOUR_ACCESS_TOKEN" -H "Content-Type": "application/json" https://api.surveymonkey.net/v3/contacts -d "{ "first_name": "John", "last_name": "Doe", "email": "test%40surveymonkey.com" }"
```

```python
import requests

s = requests.session()
s.headers.update({
  "Authorization": "Bearer %s" % YOUR_ACCESS_TOKEN,
  "Content-Type": "application/json"
})

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
url = "https://api.surveymonkey.net/v3/contacts" 
s.post(url, json=payload)
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
 * `GET`: Returns a list of all contacts. Public App users need access to the **View Contacts** [scope](#scopes)
 * `POST`: Creates a new contact, contacts can be sent survey invite messages using an email invite collector, see [Collectors and Invite Messages](#collectors-and-invite-messages). Public App users need access to the **Create/Modify Contacts** [scope](#scopes) 

####Optional Query Strings for GET

Name | Description | Data Type
------ | ------- | -------
page | Page number. Defaults to 1 | Integer
per_page | Number of contacts to return per page | Integer
status | Filter by status (default=active): '`active`, `optout`, or `bounced` | String-ENUM
sort_by | Field used to sort returned contact list (default=email): `email`, `first_name`, `last_name`, `1`, ..., `6`  | String-ENUM
sort_order | Sort order: `ASC` or `DESC` | String-ENUM
search_by | Field used to search returned contact list: `email`, `first_name`, `last_name`, `1`, ..., `6` | String-ENUM
search | Query used to search | String

####Contacts List Resource

Name |Description | Data Type
------ | ------- | -------
data[\_].id | Contact id | String
data[\_].first_name | Contact first name | String
data[\_].last_name | Contact last name | String
data[\_].email | Contact email address | String
data[\_].href | Resource API URL | String

####Request Body Arguments for POST

Name | Required | Description | Data Type
------ | ------- | ------- | -------
first_name | Yes | Contact first name | String
last_name | Yes | Contact last name | String
email | Yes | Contact email address | String
custom_fields | No | Contact custom field | Object

###/contacts/bulk

>Definition

```
POST https://api.surveymonkey.net/v3/contacts/bulk
```

>Example Request

```shell
curl -i -X POST -H "Authorization:bearer YOUR_ACCESS_TOKEN" -H "Content-Type": "application/json" https://api.surveymonkey.net/v3/contacts -d "{ "contacts": [{ "first_name": "John", "last_name": "Doe", "email": "test%40surveymonkey.com" }"
```

```python
import requests

s = requests.session()
s.headers.update({
  "Authorization": "Bearer %s" % YOUR_ACCESS_TOKEN,
  "Content-Type": "application/json"
})

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
url = "https://api.surveymonkey.net/v3/contacts/bulk"
s.post(url, json=payload)
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

 * `GET`: Returns a list of all contacts with all available fields. Public App users need access to the **View Contacts** [scope](#scopes)
 * `POST`: Creates multiple contacts, contacts can be sent survey invite messages using an email invite collector, see [Collectors and Invite Messages](#collectors-and-invite-messages). Public App users need access to the **Create/Modify Contacts** [scope](#scopes)

####Contacts List Resource

Name | Description | Data Type
------ | ------- | -------
data[\_].id | Contact id | String
data[\_].first_name | Contact first name | String
data[\_].last_name | Contact last name | String
data[\_].email | Contact email address | String
data[\_].custom_fields | Contact custom fields | Object
data[\_].href | Resource API URL | String

####Request Body Arguments for POST

Name | Required | Description | Data Type
------ | ------- | ------- | -------
data[\_].first_name | Yes | Contact first name | String
data[\_].last_name | Yes | Contact last name | String
data[\_].email | Yes | Contact email | String
data[\_].custom_fields | No | Custom contact fields | Object


###/contacts/{id}

>Definition

```
GET https://api.surveymonkey.net/v3/contacts/{contact_id}
```

>Example Request

```shell
curl -i -X GET -H "Authorization:bearer YOUR_ACCESS_TOKEN" -H "Content-Type": "application/json" https://api.surveymonkey.net/v3/contacts/1234
```

```python
import requests

s = requests.session()
s.headers.update({
  "Authorization": "Bearer %s" % YOUR_ACCESS_TOKEN,
  "Content-Type": "application/json"
})

url = "https://api.surveymonkey.net/v3/contacts/%s" % (contact_id)
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
 * `GET`: Returns a contact. Public App users need access to the **View Contacts** [scope](#scopes)
 * `PATCH`: Modifies a contact (updates any fields accepted as arguments to `POST` [/contacts](#contacts). Public App users need access to the **Create/Modify Contacts** [scope](#scopes)
 * `PUT`: Replaces a contact (same arguments and requirements as `POST`[/contacts](#contacts)). Public App users need access to the **Create/Modify Contacts** [scope](#scopes)
 * `DELETE`: Deletes a contact. Public App users need access to the **Create/Modify Contacts** [scope](#scopes)


####Contact Resource

Name | Description | Data Type
------ | ------- | -------
id | Contact id | String
first_name | Contact first name | String
last_name | Contact last name | String
email | Contact email address | String
custom_fields | Contact custom fields | Object


###/contact_fields

>Definition

```
GET https://api.surveymonkey.net/v3/contact_fields
```

>Example Request

```shell
curl -i -X GET -H "Authorization:bearer YOUR_ACCESS_TOKEN" -H "Content-Type": "application/json" https://api.surveymonkey.net/v3/contact_fields
```

```python
import requests

s = requests.session()
s.headers.update({
  "Authorization": "Bearer %s" % YOUR_ACCESS_TOKEN,
  "Content-Type": "application/json"
})

url = "https://api.surveymonkey.net/v3/contact_fields" 
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
    }],
  "links": {
    "self": "https://api.surveymonkey.net/v3/contact_fields?page=1&per_page=1"
  }
}
```

####Available Methods

 * `HEAD`: Checks if resource is available
 * `OPTIONS`: Returns available methods and options
 * `GET`: Returns a list of all [custom contacts fields](http://help.surveymonkey.com/articles/en_US/kb/Custom-Data). Public App users need access to the **View Contacts** [scope](#scopes)

####Optional Query Strings for GET

Name | Description | Data Type
------ | ------- | -------
page | Page number. Defaults to 1 | Integer
per_page | Number of contacts to return per page | Integer

####Contacts List Resource

Name |Description | Data Type
------ | ------- | -------
data[\_].id | Contact id | String
data[\_].label | Contact Field Label | String
data[\_].href | Resource API URL | String


###/contact_fields/{id}

>Definition

```
PATCH https://api.surveymonkey.net/v3/contact_fields/{contact_field_id}
```

>Example Request

```shell
curl -i -X PATCH -H "Authorization:bearer YOUR_ACCESS_TOKEN" -H "Content-Type": "application/json" https://api.surveymonkey.net/v3/contact_fields/1 -d "{"label: "5"}"
```

```python
import requests

s = requests.session()
s.headers.update({
  "Authorization": "Bearer %s" % YOUR_ACCESS_TOKEN,
  "Content-Type": "application/json"
})

payload = {
  "label" = "address"
}
url = "https://api.surveymonkey.net/v3/contact_fields/1" 
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
 * `GET`: Returns the specified [custom contact field](http://help.surveymonkey.com/articles/en_US/kb/Custom-Data). Public App users need access to the **View Contacts** [scope](#scopes)
 * `PATCH`: Modifies a [custom contact field's](http://help.surveymonkey.com/articles/en_US/kb/Custom-Data) label. Public App users need access to the **Create/Modify Contacts** [scope](#scopes)

####Request Body Arguments for PATCH

Name | Required | Description | Data Type
------ | ------- | ------- | -------
label | Yes | Label assigned to the custom contact field | String


####Contact Field Resource

Name | Description | Data Type
------ | ------- | -------
id | Contact field id | String
label | Contact field Label | String

