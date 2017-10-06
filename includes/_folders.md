##Survey Folders

Folders are used to organize surveys. The following endpoints let you retreive and create folders. Add surveys to a certain folder with a POST, PUT, or PATCH to [/surveys](#surveys) including it's `folder_id`. You can also filter surveys by folders using `folder_id` as a query parameter on GET [/surveys](#surveys). 

###/survey_folders

>Definition

```
POST https://api.surveymonkey.net/v3/survey_folders

```

>Example Request

```shell 

curl -i -X POST -H "Authorization: bearer YOUR_ACCESS_TOKEN" -H "content-Type":"application/json" https://api.surveymonkey.net/v3/survey_folders -d "{"title":"My Team Folder"}"

```


```python

import requests

s = request.session()
s.headers.update({
  "Authorization":"Bearer %s" % YOUR_ACCESS_TOKEN,
  "Content-Type":"application/json"
})

payload = {
  "title":"My Team's Folder"
}
url = "https://api.surveymonkey.net/v3/survey_folders"
s.post(url, json=payload)
```

####Response

{  
   "title":"My Team Folder",
   "href":"https:\/\/api.surveymonkey.net\/v3\/survey_folders\/1605642",
   "id":"1605642",
   "num_surveys":0
}


```

####Available Methods

 * `HEAD`: Checks if resource is available
 * `OPTIONS`: Returns available methods and options
 * `POST`: Creates 
 * `GET`: Returns available folders 


####Optional Query Strings for GET

Name | Description | Data Type
------ | ------- | -------
page | Which page of resources to return. Defaults to 1 | Integer
per_page | Number of resources to return per page. | Integer


####Survey Folders List Resource

Name | Description | Data Type
------ | ------- | -------
per_page||Integer
total||Integer
data[\_].href||String  
data[\_].num_surveys||Integer
data[\_].id||String
data[\_].title||String
page||Integer
links[\_].self||String


####Request Body Arguments for POST

Name | Required |Description | Data Type
----- | ------ |------ | -----
Title | No | Title for the folder | String