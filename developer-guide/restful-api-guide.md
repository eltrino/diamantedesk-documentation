---
title: RESTful API Guide
---

DiamanteDesk REST APIs enable interaction between the application and other software products, such as websites, CRMs, content management systems and other applications. Using the DiamanteDesk REST APIs you can read, modify, add and delete the data directly in the helpdesk.

To ensure secure access it is recommended to use HTTPS protocol for API requests.

## API Endpoints

API endpoints define the connection point to your service, giving the external application access to DiamanteDesk data. API endpoints are prefixed with your domain name:

{% highlight http %}

http(s)://domainname/rest/api/{version}/desk/

{% endhighlight %}

## Authentication

DiamanteDesk uses [WSSE authentication](https://en.wikipedia.org/wiki/WS-Security) to ensure secure access to the third party applications via REST APIs. WSSE authentication in DiamanteDesk application, which is based on Symfony, is implemented by using this [bundle](https://github.com/escapestudios/EscapeWSSEAuthenticationBundle).

WSSE authentication is based on:

* a username;
* a nonce (created to avoid replay attacks);
* a timestamp;
* the password digest (In DiamanteDesk the password digest is represented as API Key. To learn how to generate API key, please check the **API Credentials** article in the **Integration** section of DiamanteDesk documentation).

## Format

All the data in DiamanteDesk APIs is transmitted either in JSON or XML format with JSON being a default format.
The format can be specified either:

* in the request header (Content-Type, Accept). _Note:_ The MIME type shall be specified in header (application/json, application/xml).
* or specified in the URL.

## Pagination, Sorting, Filtering

### Pagination

When a user performs a request to get a collection of entities or a certain entity, the data requested is returned in the response body. Depending on the requested items, objects or products, the list of results can contain thousands of results that should be paged through. The number of items per each page can be specified using page parameters. Paginated queries start at page 1 by default. 

For example, if you set the page limit to 10 items and you need to retrieve items from 21 to 30 your request should contain such parameters: limit=10 and page=3.

When a user requests a list of certain entities, the server returns the results along with additional metadata, such as:

* the general amount of entities, shown at the X-Total HTTP header;
* the links to the connected pages in the Link HTTP header. There are 4 types of such links:

Name  | Description
------------- | -------------
next  | The URL to the following results page.
last | The URL to the last results page.
first | The URL to the first results page.
prev | The URL to the previous results page.

Take a look at the example, containing such headers:

{% highlight http %}

HTTP/1.1 200 OK

Link: <http://hostname/api/rest/latest/desk/branches?limit=25&page=2>; rel="next", <http://hostname/api/rest/latest/desk/branches?limit=25&page=5>; rel="last"
X-Total: 110 

{% endhighlight %}

### Sorting

The results can be sorted according to the **sort** and **order** GET parameters, included in the URL. The **sort** parameter performs the sorting according to the property name of an entity, **order** parameter may be set either to **asc** (ascending) or **desc** (descending).

### Filtering

Filtering can be performed according to any parameter of the corresponding entity. For example, to filter the branch by its key, add "key=PO" parameter to the URL.
 
If the value is specified for string property, the search is performed for any occurrence, meaning the result will return PO, DPO, DPOD, etc. If the value is specified for numeric property the search is performed for equal value.

To filter the results by the time when a certain entity or entities were created or updated, the following parameters should be used:

* createdBefore
* createdAfter
* updatedBefore
* updatedAfter

## Error Handling

When the fault occurs within the application or on a server side, the server returns the corresponding status code followed by the message, indicating the root cause in the response body.

Here are the status codes of the errors that may occur when working with DiamanteDesk application.

Status Code | Description
------------- | :-------------
**400**  | Validation failed and the request provided by the client was incorrect or distorted and the server could not understand it.
**401** | Such error occurs when a user attempts to access a page or resource that requires authentication. To resolve this issue, correct log in details shall be provided.
**403** | Authorization issue, meaning that a user has not been granted permission to access specific page or method.
**404** | This error means that the server could not process client request with the reason for that described in the error message.
**500** | Internal server error. This status code indicates that this is not a client-side issue, meaning that the problem occurred on the server side rather than in DiamanteDesk application. 

Take a look at the example of a 404 error below:

{% highlight yaml %}

POST /diamantedesk-1.0/web/api/rest/latest/desk/branches HTTP/1.1

{
    "name": "Test Branch",
    "description": "Test Description",
    "tags": [
        "Test Tag",
        "TB1"
    ],
    "key": "BRANCHTEST"
}

HTTP/1.1 404 Not Found

{
    "error": "Branch key already exists. Please, provide another one."
}

{% endhighlight %}

## Resources

REST APIs are necessary when DiamanteDesk is integrated into another application and when interactions with the DiamanteDesk server shall be scripted.

>NOTE: Here are the values of the variables API methods:
>
>|Variable|       Requirements          
|:------------- |:---------------| 
|   {version}   | latest, v1 |
|{_format} | xml, json |

### Branches

###### GET: Retrieve the list of all branches

{% highlight sh %}
GET /api/rest/{version}/desk/branches
{% endhighlight %}
    
**Response**
    
**Status Code:** 200 (OK)

_Response body:_ 

{% highlight yaml %}
[
    {
        "created_at": "2015-07-17T11:25:21+0000",
        "description": "branchDescription1",
        "id": 1,
        "key": "BRANCHB",
        "name": "branchName1",
        "updated_at": "2015-07-17T11:25:21+0000"
    },
    {
        "created_at": "2015-07-17T11:25:21+0000",
        "description": "branchDescription2",
        "id": 2,
        "key": "BRANCHC",
        "name": "branchName2",
        "updated_at": "2015-07-17T11:25:21+0000"
    }
]
{% endhighlight %}
    
######  GET: Retrieve a branch by ID

{% highlight sh %}
GET /api/rest/{version}/desk/branches/{id}
{% endhighlight %}
    
**Response**
    
**Status Code:** 200 (OK)

_Response body:_ 

{% highlight yaml %}
{
    "created_at": "2015-07-17T11:25:36+0000",
    "description": "Test Description",
    "id": 11,
    "key": "BRANCHTEST",
    "name": "Test Branch",
    "updated_at": "2015-07-17T11:25:36+0000"
}
{% endhighlight %}

**Status Code:** 404 (Not Found)

_Response body:_ 

{% highlight yaml %}
{
    "error": "Branch loading failed. Branch not found."
}
{% endhighlight %}

###### POST: Create a new branch

{% highlight sh %}
POST /api/rest/{version}/desk/branches
{% endhighlight %}
    
**Parameters**

| Name  | Type  |Description |Note|
|:------------- |:---------------|:-------------|:----|
| name    | _string_ | **Required.** Specify the name of a new branch. | Minimum length is 2 letters.
| description    |   _string_       |Enter the description of a new branch, if necessary. |
| tags | _arrey of strings_      | Specify the tags appropriate for the new branch. To learn more about tagging in DiamanteDesk, please check the **Tagging** section in the **User Guide** section. |
| key | _string_ | Enter the key of a new branch. Note that the key should be unique accross the whole system. | The branch key must contain only letters. Minimum length is 2 letters.

_Request example:_ 

{% highlight yaml %}
{
    "name": "Test Branch",
    "description": "Test Description",
    "tags": [
        "Test Tag"
    ],
    "key": "BRANCHTEST"
}
{% endhighlight %}
    
**Response**
    
**Status Code:** 201 (Created)

_Response body:_ 

{% highlight yaml %}
{
    "created_at": "2015-07-17T11:25:36+0000",
    "description": "Test Description",
    "id": 11,
    "key": "BRANCHTEST",
    "name": "Test Branch",
    "tags": [
        "Test Tag"
    ],
    "updated_at": "2015-07-17T11:25:36+0000"
}
{% endhighlight %}

###### PUT, PATCH: Update properties of a certain branch by its ID

{% highlight sh %}
PUT|PATCH /api/rest/{version}/desk/branches/{id}
{% endhighlight %}
    
_Request example:_ 

{% highlight yaml %}
{
    "name": "Test Branch PUT",
    "description": "Test Description",
    "tags": [
        "Test Tag"
    ]
}
{% endhighlight %}
    
**Response**
    
**Status Code:** 200 (OK)

_Response body:_ 

{% highlight yaml %}
{
    "created_at": "2015-07-17T11:25:36+0000",
    "description": "Test Description",
    "id": 11,
    "key": "BRANCHTEST",
    "name": "Test Branch PUT",
    "tags": [
        "Test Tag"
    ],
    "updated_at": "2015-07-17T11:25:36+0000"
}
{% endhighlight %}

###### DELETE: Delete a branch by ID

{% highlight sh %}
DELETE /api/rest/{version}/desk/branches/{id}
{% endhighlight %}
    
**Response**
    
**Status Code:** 204 (No Content)

_Response body:_ null

### Tickets

###### GET: Retrieve list of all tickets

{% highlight sh %}
GET /api/rest/{version}/desk/tickets
{% endhighlight %}

**Response**
    
**Status Code:** 200 (OK)

_Response body:_ 

{% highlight yaml %}
[
    {
        "assignee": 1,
        "branch": 1,
        "created_at": "2015-07-17T11:25:21+0000",
        "id": 1,
        "key": "BRANCHB-1",
        "priority": "medium",
        "reporter": "oro_1",
        "source": "phone",
        "status": "new",
        "subject": "ticketSubject1",
        "unique_id": {
            "id": "8d5fb1d682fecd97b0f4b6f050e2a8b9"
        },
        "updated_at": "2015-07-17T11:25:21+0000"
    },
    {
        "assignee": 1,
        "branch": 2,
        "created_at": "2015-07-17T11:25:21+0000",
        "id": 2,
        "key": "BRANCHC-1",
        "priority": "medium",
        "reporter": "oro_1",
        "source": "phone",
        "status": "open",
        "subject": "ticketSubject2",
        "unique_id": {
            "id": "9beddad8ecd692841ea8c8f8910b538b"
        },
        "updated_at": "2015-07-17T11:25:21+0000"
    }
]
{% endhighlight %}

###### GET: Retrieve the ticket by the given ticket ID

{% highlight sh %}
GET /api/rest/{version}/desk/tickets/{id}
{% endhighlight %}
   
**Response**
    
**Status Code:** 200 (OK)

_Response body:_ 

{% highlight yaml %}
{
    "attachments": [

    ],
    "branch": 1,
    "comments": [

    ],
    "created_at": "2015-07-17T11:25:47+0000",
    "description": "Test Description",
    "id": 12,
    "key": "BRANCHB-3",
    "priority": "medium",
    "reporter": "oro_1",
    "source": "phone",
    "status": "open",
    "subject": "Test Ticket",
    "unique_id": {
        "id": "4b1573586e00d7760babf2aa0bdb9cdc"
    },
    "updated_at": "2015-07-17T11:25:47+0000"
}
{% endhighlight %}

**Status Code:** 404 (OK)

_Response body:_   

{% highlight yaml %}
{
    "error": "Ticket loading failed, ticket not found."
}  
{% endhighlight %}

###### POST: Create a new ticket

{% highlight sh %}
POST /api/rest/{version}/desk/tickets
{% endhighlight %}
    
**Parameters**

| Name  | Type  | Description | Note|
|:------------- |:---------------|:-------------|:---|
| branch     | _integer_ | **Required.** Specify a branch name where the ticket should be created.
| subject     | _string_ | **Required.** Enter a short description of a new ticket.|
| description | _string_ | **Required.** Enter the detailed description of a new ticket.
| status | _string_ |**Required.** The available statuses are: **New**, **Open**, **Pending**, **In progress**, **Closed** and **On Hold**.
| priority | _string_ |**Required.** Specify the priority of a new ticket. The available options are **Low**, **Medium** or **High**.
| source | _string_ |**Required.** Every service user has 4 available options to contact the Help Desk team: by creating a request through a **Web** form or through the embedded form on a website (optional), as an **Email** notification, via a **Phone** call. Specify the corresponding source of a ticket.
| reporter| _string_ |**Required.** The reporter is an administrator who can create a ticket for any customer. |The name of the reporter must contain only letters.
|tags | _array of strings_ | Specify the tags appropriate for the new branch. To learn more about tagging in DiamanteDesk, please check the **Tagging** section in the **User Guide** section. |
    
_Request example:_

{% highlight yaml %}
{
    "branch": 1,
    "subject": "Test Ticket from API",
    "description": "Test Description",
    "status": "open",
    "priority": "medium",
    "source": "phone",
    "reporter": "oro_1",
    "tags" : ["test1","test2","test3","test4"]
}
{% endhighlight %}

**Response**
    
**Status Code:** 201 (Created)

_Response body:_ 

{% highlight yaml %}
{
  "attachments": [],
  "branch": 1,
  "comments": [],
  "created_at": "2015-07-31T11:26:51+0000",
  "description": "Test Description",
  "id": 95,
  "key": "BRANCHB-10",
  "priority": "medium",
  "reporter": "oro_1",
  "source": "phone",
  "status": "open",
  "subject": "Test Ticket from API",
  "tags": [
    "test1",
    "test2",
    "test3",
    "test4"
  ],
  "unique_id": {
    "id": "acee0fb73b9c1188472787b20a2760ae"
  },
  "updated_at": "2015-07-31T11:26:51+0000",
  "watcher_list": []
}
{% endhighlight %}
    
    
###### PUT, PATCH: Update certain properties of the ticket by ID

{% highlight sh %}
PUT, PATCH /api/rest/{version}/desk/tickets/{id}
{% endhighlight %}
    
_Request example:_

{% highlight yaml %}
{
   "subject": "New test subject",
   "tags": ["new test tag1", "new test tag2"]
}
{% endhighlight %}
    
**Response**
    
**Status Code:** 200 (OK)

_Response body:_ 

{% highlight yaml %}
{
  "attachments": [],
  "branch": 1,
  "comments": [],
  "created_at": "2015-07-31T11:26:51+0000",
  "description": "Test Description",
  "id": 95,
  "key": "BRANCHB-10",
  "priority": "medium",
  "reporter": "oro_1",
  "source": "phone",
  "status": "open",
  "subject": "New test subject",
  "tags": [
    "new test tag1",
    "new test tag2"
  ],
  "unique_id": {
    "id": "acee0fb73b9c1188472787b20a2760ae"
  },
  "updated_at": "2015-07-31T11:26:51+0000",
  "watcher_list": [
    {
      "id": 23,
      "user_type": "oro_1"
    }
  ]
}
{% endhighlight %}
    
###### DELETE: Delete the ticket by ID

{% highlight sh %}
DELETE /api/rest/{version}/desk/tickets/{id}  
{% endhighlight %} 
    
**Response**

**Status Code:** 204 (No Content)

_Response body:_ null
    
    
###### GET: Retrieve a ticket by the given ticket key

{% highlight sh %}
GET /api/rest/{version}/desk/tickets/{key}
{% endhighlight %}
   
**Response**
    
**Status Code:** 200 (OK)

_Response body:_ 

{% highlight yaml %}
{
    "attachments": [

    ],
    "branch": 1,
    "comments": [

    ],
    "created_at": "2015-07-17T11:25:47+0000",
    "description": "Test Description",
    "id": 12,
    "key": "BRANCHB-3",
    "priority": "medium",
    "reporter": "oro_1",
    "source": "phone",
    "status": "open",
    "subject": "Test Ticket",
    "unique_id": {
        "id": "4b1573586e00d7760babf2aa0bdb9cdc"
    },
    "updated_at": "2015-07-17T11:25:47+0000"
}
{% endhighlight %}
    
**Status Code:** 404 (Not Found)

_Response body:_ 

{% highlight yaml %}
}
    "error": "Ticket loading failed, ticket not found."
}
{% endhighlight %}

###### PUT, PATCH: Update certain properties of a ticket by the ticket key

{% highlight sh %}
PUT, PATCH /api/rest/{version}/desk/tickets/{key}
{% endhighlight %}
    
_Request example:_

{% highlight yaml %}
{
   "subject": "New test subject",
   "tags": ["new test tag5", "new test tag6"]
}
{% endhighlight %}
   
**Response**
    
**Status Code:** 200 (OK)

_Response body:_ 

{% highlight yaml %}
{
  "attachments": [],
  "branch": 1,
  "comments": [],
  "created_at": "2015-07-31T11:26:51+0000",
  "description": "Test Description",
  "id": 95,
  "key": "BRANCHB-10",
  "priority": "medium",
  "reporter": "oro_1",
  "source": "phone",
  "status": "open",
  "subject": "New test subject",
  "tags": [
    "new test tag5",
    "new test tag6"
  ],
  "unique_id": {
    "id": "acee0fb73b9c1188472787b20a2760ae"
  },
  "updated_at": "2015-07-31T11:26:51+0000",
  "watcher_list": [
    {
      "id": 23,
      "user_type": "oro_1"
    }
  ]
}
{% endhighlight %}
    
###### DELETE: Delete the ticket by the ticket key

{% highlight sh %}
DELETE /api/rest/{version}/desk/tickets/{key} 
{% endhighlight %}
    
**Response**

**Status Code:** 204 (No Content)

_Response body:_ null 

###### GET: Retrieve the list of ticket attachments by ticket ID

{% highlight sh %}
GET /api/rest/{version}/desk/tickets/{id}/attachments
{% endhighlight %}
    
**Response**
    
**Status Code:** 200 (OK)

_Response body:_ 

{% highlight yaml %}  
[
    {
        "id": 15,
        "created_at": "2015-07-17T11:25:53+0000",
        "updated_at": "2015-07-17T11:25:53+0000",
        "file": {
            "url": "http:\/\/localhost\/desk\/attachments\/download\/file\/450385ca08c7cfe5b507ad85f3a17428",
            "filename": "test.jpg"
        },
        "thumbnails": {
            "url": "http:\/\/localhost\/desk\/attachments\/download\/thumbnail\/450385ca08c7cfe5b507ad85f3a17428",
            "filename": "450385ca08c7cfe5b507ad85f3a17428.png"
        }
    }
]
{% endhighlight %}

###### GET: Retrieve ticket attachments by attachment ID

{% highlight sh %}
GET /api/rest/{version}/desk/tickets/{ticketId}/attachments/{attachmentId}
{% endhighlight %}
    
**Response**
    
**Status Code:** 200 (OK)

_Response body:_ 

{% highlight yaml %} 
{
    "id": 15,
    "created_at": "2015-07-17T11:25:53+0000",
    "updated_at": "2015-07-17T11:25:53+0000",
    "file": {
        "url": "http:\/\/localhost\/desk\/attachments\/download\/file\/450385ca08c7cfe5b507ad85f3a17428",
        "filename": "test.jpg"
    },
    "thumbnails": {
        "url": "http:\/\/localhost\/desk\/attachments\/download\/thumbnail\/450385ca08c7cfe5b507ad85f3a17428",
        "filename": "450385ca08c7cfe5b507ad85f3a17428.png"
    }
}
{% endhighlight %}
    
**Status Code:** 404 (Not Found)

_Response body:_

{% highlight yaml %} 
{
    "error": "Attachment loading failed. Ticket has no such attachment."
}
{% endhighlight %}   
    
###### POST: Add attachment to the ticket

{% highlight sh %}
POST /api/rest/{version}/desk/tickets/{ticketId}/attachments
{% endhighlight %}

_Request example:_

{% highlight yaml %} 
{
    "attachmentsInput": [
        {
            "filename": "test.jpg",
            "content": "R0lGODlhAQABAIAAAAUEBAAAACwAAAAAAQABAAACAkQBADs="
        }
    ]
}
{% endhighlight %}
    
**Response**
    
**Status Code:** 201 (Created)

_Response body:_ 

{% highlight yaml %}
[
    {
        "id": 15,
        "created_at": "2015-07-17T11:25:53+0000",
        "updated_at": "2015-07-17T11:25:53+0000",
        "file": {
            "url": "http:\/\/localhost\/desk\/attachments\/download\/file\/450385ca08c7cfe5b507ad85f3a17428",
            "filename": "test.jpg"
        },
        "thumbnails": {
            "url": "http:\/\/localhost\/desk\/attachments\/download\/thumbnail\/450385ca08c7cfe5b507ad85f3a17428",
            "filename": "450385ca08c7cfe5b507ad85f3a17428.png"
        }
    }
]
{% endhighlight %}
    
###### DELETE: Remove Attachment from the ticket

{% highlight sh %}
DELETE /api/rest/{version}/desk/tickets/{ticketId}/attachments/{attachmentId}
{% endhighlight %}
    
**Response**
    
**Status Code:** 204 (No Content)

_Response body:_ null


###### GET: Retrieve personal data based on the provided ticket ID

{% highlight sh %}
GET /api/rest/{version}/desk/ticket/{id}/assignee
{% endhighlight %}

**Response**
    
**Status Code:** 200 (OK)

_Response body:_ 

{% highlight yaml %}
{
  "email": "pol.vova@gmail.com",
  "name": "asdasd dasdasd",
  "id": "oro_1"
}
{% endhighlight %}

### Comments

###### GET: Retrieve the list of all comments

{% highlight sh %}
GET /api/rest/{version}/desk/comments
{% endhighlight %}
    
**Response**
    
**Status Code:** 200 (OK)

_Response body:_ 

{% highlight yaml %}
[
    {
        "attachments": [

        ],
        "author": 1,
        "author_type": "oro",
        "content": "commentContent1-1",
        "created_at": "2015-07-17T11:25:22+0000",
        "id": 1,
        "private": false,
        "ticket": 1,
        "updated_at": "2015-07-17T11:25:22+0000"
    },
    {
        "attachments": [

        ],
        "author": 1,
        "author_type": "oro",
        "content": "commentContent1-2",
        "created_at": "2015-07-17T11:25:22+0000",
        "id": 2,
        "private": false,
        "ticket": 1,
        "updated_at": "2015-07-17T11:25:22+0000"
    }
]
{% endhighlight %}

###### GET: Retrieve the comment by the given comment ID

{% highlight sh %}
GET /api/rest/{version}/desk/comments/{id}
{% endhighlight %}
        
**Response**
    
**Status Code:** 200 (OK)

_Response body:_ 

{% highlight yaml %}
{
    "attachments": [

    ],
    "author": 10,
    "author_type": "diamante",
    "content": "Test Comment",
    "created_at": "2015-07-17T11:25:22+0000",
    "id": 101,
    "private": false,
    "ticket": 1,
    "updated_at": "2015-07-17T11:25:22+0000"
}
{% endhighlight %}    
    
**Status Code:** 404 (OK)

_Response body:_   

{% highlight yaml %}
{
    "error": "Comment loading failed, comment not found."
} 
{% endhighlight %}   
    
###### POST: Add a new comment to the ticket.

{% highlight sh %}
POST /api/rest/{version}/desk/comments
{% endhighlight %}
 
 **Parameters**   
    
| Name  | Type  | Description | Note
|:------------- |:---------------|:-------------|:---|
| content     | _string_ | **Required.** Add your comment into this section. |
| ticket     | _integer_       |**Required.** Provide the ID of a ticket where the comment is added. |
| author | _string_       | **Required.** Specify the name of a user who adds the comment to the ticket. |The name of an author must contain only letters.|
| ticketStatus | _string_ | **Required.** Specify the status of a ticket after the new comment is added to it. The available statuses are: **New**, **Open**, **Pending**, **In progress**, **Closed** and **On Hold**.
    
_Request example:_

{% highlight yaml %}
{
    "content": "Test Comment",
    "ticket": 1,
    "author": "oro_1",
    "ticketStatus": "new"
}  
{% endhighlight %}  
    
**Response**
    
**Status Code:** 201 (Created)

_Response body:_ 

{% highlight yaml %}
{
    "attachments": [

    ],
    "author": 1,
    "author_type": "oro",
    "content": "Test Comment",
    "created_at": "2015-07-17T11:25:42+0000",
    "id": 104,
    "private": false,
    "ticket": 1,
    "updated_at": "2015-07-17T11:25:42+0000"
}

{% endhighlight %}
    
###### PUT, PATCH: Update certain properties of the comment be the comment ID

{% highlight sh %}
PUT|PATCH /api/rest/{version}/desk/comments/{id}
{% endhighlight %}
    
**Response**
    
**Status Code:** 200 (OK)

_Request example:_

{% highlight yaml %}
{
    "content": "Test Comment Updated PUT",
    "ticketStatus": "closed"
}
{% endhighlight %}

_Response body:_ 

{% highlight yaml %}
{
    "attachments": [

    ],
    "author": 10,
    "author_type": "diamante",
    "content": "Test Comment Updated PUT",
    "created_at": "2015-07-17T11:25:22+0000",
    "id": 101,
    "private": false,
    "ticket": 1,
    "updated_at": "2015-07-17T11:25:22+0000"
}
{% endhighlight %}

###### DELETE: Delete a ticket comment by the comment ID

{% highlight sh %}
DELETE /api/rest/{version}/desk/comments/{id}
{% endhighlight %}
    
**Response**

**Status Code:** 204 (No Content)

_Response body:_ null 

###### GET: Retrieve the information about the comment author based on the provided comment ID

{% highlight sh %}
GET /api/rest/{version}/desk/comment/{id}/author
{% endhighlight %}

**Response**
    
**Status Code:** 200 (OK)

_Response body:_

{% highlight yaml %}
{
  "email": "pol.vova@gmail.com",
  "name": "asdasd dasdasd",
  "id": "oro_1"
}
{% endhighlight %}

###### GET: Retrieve all comment attachments

{% highlight sh %}
GET /api/rest/{version}/desk/comments/{id}/attachments
{% endhighlight %}

**Response**
    
**Status Code:** 200 (OK)

_Response body:_

{% highlight yaml %}
[
    {
        "id": 12,
        "created_at": "2015-07-17T11:25:27+0000",
        "updated_at": "2015-07-17T11:25:27+0000",
        "file": {
            "url": "http:\/\/localhost\/desk\/attachments\/download\/file\/61fcb86ab5a53db412b2f3823f8a20ac",
            "filename": "test.jpg"
        },
        "thumbnails": {
            "url": "http:\/\/localhost\/desk\/attachments\/download\/thumbnail\/61fcb86ab5a53db412b2f3823f8a20ac",
            "filename": "61fcb86ab5a53db412b2f3823f8a20ac.png"
        }
    }
]
{% endhighlight %}

###### Retrieve comment attachments by the attachment ID

{% highlight sh %}
GET /api/rest/{version}/desk/comments/{commentId}/attachments/{attachmentId}
{% endhighlight %}
    
**Response**
    
**Status Code:** 200 (OK)

_Response body:_

{% highlight yaml %}
{
    "id": 12,
    "created_at": "2015-07-17T11:25:27+0000",
    "updated_at": "2015-07-17T11:25:27+0000",
    "file": {
        "url": "http:\/\/localhost\/desk\/attachments\/download\/file\/61fcb86ab5a53db412b2f3823f8a20ac",
        "filename": "test.jpg"
    },
    "thumbnails": {
        "url": "http:\/\/localhost\/desk\/attachments\/download\/thumbnail\/61fcb86ab5a53db412b2f3823f8a20ac",
        "filename": "61fcb86ab5a53db412b2f3823f8a20ac.png"
    }
}
{% endhighlight %}

**Status Code:** 404 (OK)

_Response body:_   

{% highlight yaml %}
{
    "error": "Attachment loading failed. Comment has no such attachment."
}
{% endhighlight %}

###### POST: Add attachment to the comment

{% highlight sh %}
POST /api/rest/{version}/desk/comments/{commentId}/attachments
{% endhighlight %}

_Request example:_

{% highlight yaml %} 
{
    "attachmentsInput": [
        {
            "filename": "test.jpg",
            "content": "R0lGODlhAQABAIAAAAUEBAAAACwAAAAAAQABAAACAkQBADs="
        }
    ]
}
{% endhighlight %}
    
**Response**
    
**Status Code:** 201 (Created)

_Response body:_

{% highlight yaml %}
[
    {
        "id": 13,
        "created_at": "2015-07-17T11:25:34+0000",
        "updated_at": "2015-07-17T11:25:34+0000",
        "file": {
            "url": "http:\/\/localhost\/desk\/attachments\/download\/file\/338477dbcd9c4faae7584cda781be854",
            "filename": "test.jpg"
        },
        "thumbnails": {
            "url": "http:\/\/localhost\/desk\/attachments\/download\/thumbnail\/338477dbcd9c4faae7584cda781be854",
            "filename": "338477dbcd9c4faae7584cda781be854.png"
        }
    }
]
{% endhighlight %}

######  DELETE: Remove the attachment from the comment by the attachment ID

{% highlight sh %}
DELETE /api/rest/{version}/desk/comments/{commentId}/attachments/{attachmentId}
{% endhighlight %}
    
**Response**

**Status Code:** 204 (No Content)

_Response body:_ null

### Users

###### GET: Retrieve the list of all users

{% highlight sh %}
GET /api/rest/{version}/desk/users
{% endhighlight %}
    
**Response**
    
**Status Code:** 200 (OK)

_Response body:_

{% highlight yaml %}
[
    {
        "id": 1,
        "email": "sdasdasd@asfasf.com",
        "first_name": "das",
        "last_name": "dasda"
    },
    {
        "id": 2,
        "email": "vladimir.polischuk@eltrino.com",
        "first_name": "\u0444\u0456\u0432\u0444\u0456\u0432",
        "last_name": "\u0432\u0444\u0456\u0432"
    }
{% endhighlight %}
    
###### POST: Create a new user

{% highlight sh %}
POST /api/rest/{version}/desk/users
{% endhighlight %}
    
**Parameters**

| Name  | Type  | Description |
|:------------- |:---------------|:-------------|
| firstName     | _string_ | **Required.** Provide the first name of a new user. |
| lastName     | _string_   | **Required.** Provide the last name of a new user.|
| email | _string_ | **Required.** Add an email of a new user. This email is going to be used for email notifications and password recovery.|
    
_Request example:_

{% highlight yaml %}
{
    "email": "1437135532dummy-test-email-address@test-server.local",
    "firstName": "John",
    "lastName": "Dou"
}
{% endhighlight %}

**Response**
    
**Status Code:** 201 (Created)

_Response body:_

{% highlight yaml %}
{
    "id": 11,
    "email": "1437135532dummy-test-email-address@test-server.local",
    "first_name": "John",
    "last_name": "Dou"
}
{% endhighlight %}
    
###### GET: Retrieve user data

{% highlight sh %}
GET /api/rest/{version}/desk/users/{email}/
{% endhighlight %}
    
**Response**
    
**Status Code:** 200 (OK)

_Response body:_

{% highlight yaml %}
{
    "id": 11,
    "email": "1437135532dummy-test-email-address@test-server.local",
    "first_name": "John",
    "last_name": "Dou"
}
{% endhighlight %}
    
**Status Code:** 404 (Not Found)
_Response body:_

{% highlight yaml %}
{
    "error": "User not found."
}
{% endhighlight %}
