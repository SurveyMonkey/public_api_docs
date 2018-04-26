##Organizations

Use these endpoints to get an organization's information, including roles and workgroups in your [team](http://help.surveymonkey.com/articles/en_US/kb/Groups) account.

###/workgroups

>Definition

```
GET https://api.surveymonkey.com/v3/workgroups
```

>Example Request

```shell
curl -i -X GET -H "Authorization:bearer YOUR_ACCESS_TOKEN" -H "Content-Type": "application/json" https://api.surveymonkey.com/v3/workgroups
```

```python
import requests

s = requests.Session()
s.headers.update({
  "Authorization": "Bearer %s" % YOUR_ACCESS_TOKEN,
  "Content-Type": "application/json"
})

url = "https://api.surveymonkey.com/v3/workgroups"
s.get(url)
```

>Example Response

```json
{
  "per_page": 50,
  "total": 1,
  "data": [{
    "is_visible": true,
    "members_count": 1,
    "description": "Spreading the company brand",
    "default_role": {
      "is_enabled": true,
      "description": "",
      "metadata": {},
      "id": "a1af2174db7c40c796f3b069d7efbc63",
      "name": "Viewer"
    },
    "created_at": "2018-04-21T21:21:46",
    "updated_at": "2018-04-21T21:21:46",
    "shares": [],
    "name": "Marketing",
    "shares_count": 0,
    "membership": {
      "status": "active",
      "is_owner": true
    },
    "members": [{
      "is_owner": true,
      "user_id": "1234567"
    }],
    "id": "71d9d408d1914c9ca85ffcda8330d675",
    "metadata": {}
  }],
  "page": 1,
  "links": {
    "self": "https://api.surveymonkey.com/v3/workgroups?page=1&per_page=50"
  }
}

```

####Available Methods

 * `HEAD`: Checks if resource is available
 * `OPTIONS`: Returns available methods and options
 * `GET`: Returns the workgroups the user can see in an organization. Public App users need access to the **View Workgroups** [scope](#scopes)
 * `POST`: Creates a new workgroup. Public App users need access to the **Create/Modify Workgroups** [scope](#scopes)

####Optional Query Strings for GET

Name | Description | Data Type
------ | ------- | -------
page | Which page of resources to return. Defaults to 1 | Integer
per_page | Number of resources to return per page | Integer

####Workgroups List Resource

Name | Description | Data Type
------ | ------- | -------
data[\_].id | ID of the workgroup | String
data[\_].name | Name of the workgroup | String
data[\_].description | Description of the workgroup | String
data[\_].is_visible | Whether the workgroup is publicly visible or only visible to its members and administrators | Boolean
data[\_].created_at | Datetime when the workgroup was created | DateTime
data[\_].updated_at | Datetime when the workgroup was last updated | DateTime
data[\_].members | The active members of the workgroup. | Array
data[\_].shares_count | Number of resources shared with the workgroup | Integer
data[\_].members_count | Number of members in the workgroup (includes non-active) | Integer
data[\_].default_role | The default role for the workgroup | Object
data[\_].membership | Membership information for the requested user | Object

####Request Body Arguments for POST

Name | Required | Description | Data Type
------ | ------- | ------- | -------
name | Yes | Name of the workgroup | String
description | Yes | Description of the workgroup | String-ENUM
is_visible | Yes | Whether the workgroup is publicly visible or only visible to its members and administrators | String

###/workgroups/{workgroup_id}

>Definition

```
GET https://api.surveymonkey.com/v3/workgroups/{workgroup_id}
```

>Example Request

```shell
curl -H "Authorization:bearer YOUR_ACCESS_TOKEN" -H "Content-Type": "application/json" https://api.surveymonkey.com/v3/workgroups/1234
```

```python
import requests

s = requests.session()
s.headers.update({
  "Authorization": "Bearer %s" % YOUR_ACCESS_TOKEN,
  "Content-Type": "application/json"
})

url = "https://api.surveymonkey.com/v3/workgroups/%s" % (workgroup_id)
s.get(url)
```

>Example Response

```json
{
  "is_visible": true,
  "members_count": 1,
  "description": "Spreading the company brand",
  "default_role": {
    "is_enabled": true,
    "description": "",
    "metadata": {},
    "id": "a1af2174db7c40c796f3b069d7efbc63",
    "name": "Viewer"
  },
  "created_at": "2018-04-21T21:21:46",
  "updated_at": "2018-04-21T21:21:46",
  "shares": [],
  "shares_count": 0,
  "membership": {
    "status": "active",
    "is_owner": true
  },
  "members": [{
    "is_owner": true,
    "user_id": "1234567"
  }],
  "metadata": {},
  "id": "71d9d408d1914c9ca85ffcda8330d675",
  "name": "Marketing"
}
```

####Available Methods

 * `HEAD`: Checks if resource is available
 * `OPTIONS`: Returns available methods and options
 * `GET`: Returns a workgroup. Public App users need access to the **View Workgroups** [scope](#scopes)
 * `PATCH`: Modifies a workgroup (updates any fields accepted as arguments to `POST` [/workgroups](#workgroups)). Public App users need access to the **Create/Modify Workgroups** [scope](#scopes)
 * `DELETE`: Deletes a workgroup. Public App users need access to the **Create/Modify Workgroups** [scope](#scopes)

####Workgroups Resource

Name | Description | Data Type
------ | ------- | -------
id | ID of the workgroup | String
name | Name of the workgroup | String
description | Description of the workgroup | String
is_visible | Whether the workgroup is publicly visible or only visible to its members and administrators | Boolean
created_at | Datetime when the workgroup was created | DateTime
updated_at | Datetime when the workgroup was last updated | DateTime
members | The active members of the workgroup. | Array
shares_count | Number of resources shared with the workgroup | Integer
members_count | Number of members in the workgroup (includes non-active) | Integer
default_role | The default role for the workgroup | Object
membership | Membership information for the requested user | Object

###/workgroups/{workgroup_id}/members

>Definition

```
GET https://api.surveymonkey.com/v3/workgroups/{workgroup_id}/members
```

>Example Request

```shell
curl -i -X GET -H "Authorization:bearer YOUR_ACCESS_TOKEN" -H "Content-Type": "application/json" https://api.surveymonkey.com/v3/workgroups/{workgroup_id}/members
```

```python
import requests

s = requests.Session()
s.headers.update({
  "Authorization": "Bearer %s" % YOUR_ACCESS_TOKEN,
  "Content-Type": "application/json"
})

url = "https://api.surveymonkey.com/v3/workgroups/%s/members" % workgroup_id
s.get(url)
```

>Example Response

```json
{
  "per_page": 50,
  "total": 1,
  "data": [{
    "workgroup_id": "71d9d408d1914c9ca85ffcda8330d675",
    "status": "active",
    "is_workgroup_owner": true,
    "created_at": "2018-04-21T21:21:46",
    "updated_at": "2018-04-21T21:21:46",
    "role_assignment_id": "a1af2174db7c40c796f3b069d7efbc63",
    "id": "1234567"
  }],
  "page": 1,
  "links": {
    "self": "https://api.surveymonkey.com/v3/workgroups/71d9d408d1914c9ca85ffcda8330d675/members?page=1&per_page=50"
  }
}
```

####Available Methods

 * `HEAD`: Checks if resource is available
 * `OPTIONS`: Returns available methods and options
 * `GET`: Returns the members in a workgroup. Public App users need access to the **View Workgroup Members** [scope](#scopes)
 * `POST`: Creates a new workgroup member. Public App users need access to the **Create/Modify Workgroup Members** [scope](#scopes)

####Optional Query Strings for GET

Name | Description | Data Type
------ | ------- | -------
page | Which page of resources to return. Defaults to 1 | Integer
per_page | Number of resources to return per page | Integer

####Workgroup Members List Resource

Name | Description | Data Type
------ | ------- | -------
data[\_].id | The user ID of the member | String
data[\_].workgroup_id | ID of the member's workgroup | String
data[\_].is_workgroup_owner | Whether the member is an owner of the workgroup | Boolean
data[\_].role_assignment_id | An ID referencing the assigned role of the member | String
data[\_].status | The status of the member, either "active" or "pending" | String-ENUM
data[\_].created_at | Datetime when the member was created | DateTime
data[\_].updated_at | Datetime when the member was last updated | DateTime

####Request Body Arguments for POST

Name | Required | Description | Data Type
------ | ------- | ------- | -------
user_id | Yes | The user ID of the new member to add | String
is_workgroup_owner | Yes | Whether the new member will be an owner of the workgroup | Boolean

###/workgroups/{workgroup_id}/members/bulk

####Available Methods

 * `HEAD`: Checks if resource is available
 * `OPTIONS`: Returns available methods and options
 * `POST`: Creates many new workgroup members. Public App users need access to the **Create/Modify Workgroup Members** [scope](#scopes)

####Request Body Arguments for POST

Name | Required | Description | Data Type
------ | ------- | ------- | -------
members[\_].user_id | Yes | The user ID of the new member to add | String
members[\_].is_workgroup_owner | Yes | Whether the new member will be an owner of the workgroup | Boolean

###/workgroups/{workgroup_id}/members/{member_id}

>Definition

```
GET https://api.surveymonkey.com/v3/workgroups/{workgroup_id}/members/{member_id}
```

>Example Request

```shell
curl -H "Authorization:bearer YOUR_ACCESS_TOKEN" -H "Content-Type": "application/json" https://api.surveymonkey.com/v3/workgroups/1234/members/1234
```

```python
import requests

s = requests.session()
s.headers.update({
  "Authorization": "Bearer %s" % YOUR_ACCESS_TOKEN,
  "Content-Type": "application/json"
})

url = "https://api.surveymonkey.com/v3/workgroups/%s/members/%s" % (workgroup_id, member_id)
s.get(url)
```

>Example Response

```json
{
  "workgroup_id": "71d9d408d1914c9ca85ffcda8330d675",
  "status": "active",
  "role_assignment_id": "a1af2174db7c40c796f3b069d7efbc63",
  "is_workgroup_owner": true,
  "created_at": "2018-04-21T21:21:46",
  "updated_at": "2018-04-21T21:21:46",
  "id": "1234567"
}
```

####Available Methods

 * `HEAD`: Checks if resource is available
 * `OPTIONS`: Returns available methods and options
 * `GET`: Returns a member. Public App users need access to the **View Workgroup Members** [scope](#scopes)
 * `PATCH`: Modifies a member (updates any fields accepted as arguments to `POST` [/workgroups/{workgroup_id}/members](#workgroups-workgroup_id-members)). Public App users need access to the **Create/Modify Workgroup Members** [scope](#scopes)
 * `DELETE`: Deletes a member from a workgroup. Public App users need access to the **Create/Modify Workgroup Members** [scope](#scopes)

####Workgroup Members Resource

Name | Description | Data Type
------ | ------- | -------
id | The user ID of the member | String
workgroup_id | ID of the member's workgroup | String
is_workgroup_owner | Whether the member is an owner of the workgroup | Boolean
role_assignment_id | An ID referencing the assigned role of the member | String
status | The status of the member, either "active" or "pending" | String-ENUM
created_at | Datetime when the member was created | DateTime
updated_at | Datetime when the member was last updated | DateTime

###/workgroups/{workgroup_id}/shares

>Definition

```
GET https://api.surveymonkey.com/v3/workgroups/{workgroup_id}/shares
```

>Example Request

```shell
curl -i -X GET -H "Authorization:bearer YOUR_ACCESS_TOKEN" -H "Content-Type": "application/json" https://api.surveymonkey.com/v3/workgroups/{workgroup_id}/shares
```

```python
import requests

s = requests.Session()
s.headers.update({
  "Authorization": "Bearer %s" % YOUR_ACCESS_TOKEN,
  "Content-Type": "application/json"
})

url = "https://api.surveymonkey.com/v3/workgroups/%s/shares" % workgroup_id
s.get(url)
```

>Example Response

```json
{
  "per_page": 50,
  "total": 1,
  "data": [{
    "workgroup_id": "71d9d408d1914c9ca85ffcda8330d675",
    "organization_id": "54321",
    "owner_user_id": "1234567",
    "resource_id": "101101101",
    "created_at": "2018-04-21T14:36:38",
    "id": "0ca749c2893245c5b96a128eee4c2d42",
    "resource_type": "survey"
  }],
  "page": 1,
  "links": {
    "self": "https://api.surveymonkey.com/v3/workgroups/71d9d408d1914c9ca85ffcda8330d675/shares?page=1&per_page=50"
  }
}
```

####Available Methods

 * `HEAD`: Checks if resource is available
 * `OPTIONS`: Returns available methods and options
 * `GET`: Returns the resources shared in a workgroup. Public App users need access to the **View Workgroup Shares** [scope](#scopes)
 * `POST`: Add a new shared resource to the workgroup. Public App users need access to the **Create/Modify Workgroup Shares** [scope](#scopes)

####Optional Query Strings for GET

Name | Description | Data Type
------ | ------- | -------
page | Which page of resources to return. Defaults to 1 | Integer
per_page | Number of resources to return per page | Integer
include | Specify additional fields to return for each resource: `permissions`, `resource_details` | Comma Separated String-ENUM

####Workgroup Shares List Resource

Name | Description | Data Type
------ | ------- | -------
data[\_].id | ID of the share record | String
data[\_].organization_id | ID of the user's organization (Team ID) | String
data[\_].workgroup_id | D of the workgroup that was shared with | String
data[\_].owner_user_id | The ID of the user who shared the resource | String
data[\_].resource_type | The type of the shared resource (e.g. `survey`) | String-ENUM
data[\_].resource_id | The ID of the shared resource (e.g. the ID of a survey) | String
data[\_].created_at | Datetime when the resource was shared | DateTime

####Request Body Arguments for POST

Name | Required | Description | Data Type
------ | ------- | ------- | -------
resource_type | Yes | The type of the shared resource, one of: `survey` | String-ENUM
resource_id | Yes | The ID of the shared resource (e.g. the ID of a survey) | String

###/workgroups/{workgroup_id}/shares/bulk

####Available Methods

 * `HEAD`: Checks if resource is available
 * `OPTIONS`: Returns available methods and options
 * `POST`: Shares a list of resources within a workgroup. Public App users need access to the **Create/Modify Workgroup Shares** [scope](#scopes)

####Request Body Arguments for POST

Name | Required | Description | Data Type
------ | ------- | ------- | -------
shares[\_].resource_type | Yes | The type of the shared resource, one of: `survey` | String-ENUM
shares[\_].resource_id | Yes | The ID of the shared resource (e.g. the ID of a survey) | String

###/workgroups/{workgroup_id}/shares/{share_id}

>Definition

```
GET https://api.surveymonkey.com/v3/workgroups/{workgroup_id}/shares/{share_id}
```

>Example Request

```shell
curl -H "Authorization:bearer YOUR_ACCESS_TOKEN" -H "Content-Type": "application/json" https://api.surveymonkey.com/v3/workgroups/1234/shares/1234
```

```python
import requests

s = requests.session()
s.headers.update({
  "Authorization": "Bearer %s" % YOUR_ACCESS_TOKEN,
  "Content-Type": "application/json"
})

url = "https://api.surveymonkey.com/v3/workgroups/%s/shares/%s" % (workgroup_id, share_id)
s.get(url)
```

>Example Response

```json
{
  "workgroup_id": "71d9d408d1914c9ca85ffcda8330d675",
  "organization_id": "54321",
  "owner_user_id": "1234567",
  "resource_id": "101101101",
  "created_at": "2018-04-21T14:36:38",
  "id": "0ca749c2893245c5b96a128eee4c2d42",
  "resource_type": "survey"
}
```

####Available Methods

 * `HEAD`: Checks if resource is available
 * `OPTIONS`: Returns available methods and options
 * `GET`: Returns a shared resource. Public App users need access to the **View Workgroup Shares** [scope](#scopes)
 * `DELETE`: Remove a resource from being shared within a workgroup. Public App users need access to the **Create/Modify Workgroup Shares** [scope](#scopes)

####Workgroup Shares Resource

Name | Description | Data Type
------ | ------- | -------
id | ID of the share record | String
organization_id | ID of the user's organization (Team ID) | String
workgroup_id | D of the workgroup that was shared with | String
owner_user_id | The ID of the user who shared the resource | String
resource_type | The type of the shared resource (e.g. `survey`) | String-ENUM
resource_id | The ID of the shared resource (e.g. the ID of a survey) | String
created_at | Datetime when the resource was shared | DateTime

###/roles

>Definition

```
GET https://api.surveymonkey.com/v3/roles
```

>Example Request

```shell
curl -i -X GET -H "Authorization:bearer YOUR_ACCESS_TOKEN" -H "Content-Type": "application/json" https://api.surveymonkey.com/v3/roles
```

```python
import requests

s = requests.Session()
s.headers.update({
  "Authorization": "Bearer %s" % YOUR_ACCESS_TOKEN,
  "Content-Type": "application/json"
})

url = "https://api.surveymonkey.com/v3/roles"
s.get(url)
```

>Example Response

```json
{
  "per_page": 50,
  "total": 2,
  "data": [{
    "is_enabled": true,
    "created_at": "2017-04-13T19:57:40",
    "description": "",
    "privileges": [
      "design.read_only",
      "collect.read_only",
      "analyze.read_only"
    ],
    "updated_at": "2017-07-11T13:04:35",
    "is_system_role": true,
    "id": "a1af2174db7c40c796f3b069d7efbc63",
    "name": "Viewer"
  }, {
    "is_enabled": true,
    "created_at": "2017-04-13T19:57:40",
    "description": "",
    "privileges": [
      "design.full_access",
      "collect.full_access",
      "analyze.full_access"
    ],
    "updated_at": "2017-06-26T13:12:11",
    "is_system_role": true,
    "id": "731fcd072de6426fba74ec7751aa6eab",
    "name": "Full Access"
  }],
  "page": 1,
  "links": {
    "self": "https://api.surveymonkey.com/v3/roles?page=1&per_page=50"
  }
}
```

####Available Methods

 * `HEAD`: Checks if resource is available
 * `OPTIONS`: Returns available methods and options
 * `GET`: Returns the list of user roles in an organization. Public App users need access to the **View Roles** [scope](#scopes)

####Optional Query Strings for GET

Name | Description | Data Type
------ | ------- | -------
page | Which page of resources to return. Defaults to 1 | Integer
per_page | Number of resources to return per page | Integer

####Roles List Resource

Name | Description | Data Type
------ | ------- | -------
data[\_].id | ID of the role | String
data[\_].name | Display name of the role | String
data[\_].description | Description of the role | String
data[\_].privileges | An array of scoped privileges granted by the role. For example, the privilege "design.full_access" grants access to all actions within the design features of surveys | Array
data[\_].is_system_role | Indicates whether the role is a system-defined (as opposed to a custom one created within your organization) | Boolean
data[\_].is_enabled | Whether the role is active for an organization. Disabled roles grant no privileges and cannot be assigned to members | Boolean
data[\_].created_at | Datetime when the role was created | DateTime
data[\_].updated_at | Datetime when the role was last updated | DateTime
