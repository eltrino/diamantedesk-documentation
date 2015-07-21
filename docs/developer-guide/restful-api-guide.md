#RESTful API Guide

DiamanteDesk REST APIs enable interaction between the application and other software products, such as websites, CRMs, content management systems and other applications. Using the DiamanteDesk REST APIs you can read, modify, add and delete the data directly in the helpdesk.

API access is performed over HTTPS protocol.

## API Endpoints

API endpoints define the connection point to your service, giving the external application access to DiamanteDesk data. API endpoints are prefixed with your domain name:

     http(s)://domainname/rest/api/{version}/desk/

## Authentication

DiamanteDesk uses [WSSE authentication](https://en.wikipedia.org/wiki/WS-Security) to ensure secure access to the third party applications via REST APIs. WSSE authentication in DiamanteDesk application, which is based on Symfony, is implemented by using this [bundle](https://github.com/escapestudios/EscapeWSSEAuthenticationBundle).

WSSE authentication is based on:

* a username;
* a nonce (created to avoid replay attacks);
* a timestamp;
* the password digest (In DidamanteDesk the password digest is represented as API Key. To learn how to generate API key, please check the **API Credentials** article in the **Integration** section of DiamanteDesk documentation).

## Format

All the data in DiamanteDesk APIs is transmitted either in JSON or XML format with JSON being a default format.
The format can be specified either:

* in the request header (Content-Type, Accept). _Note:_ The MIME type shall be specified in header (application/json, application/xml).
* or at the end of a URL.

## Pagination, Sorting, Filtering

### Pagination

When a user performs a GET request, the array of the data requested is returned in the response body. Depending on the requested items, objects or products, the list of results can contain thousands of results that should be paged through. You can specify how many items you want each page to return using page parameters. Paginated queries start at page 1 by default. 

For example, if you set the page limit to 10 items and you need to retrieve items from 21 to 30 your request should contain such parameters: limit=10 and page_no=3.

GET API methods return the total number of objects in **X-Total** before pagination is applied:

    HTTP/1.1 200 OK
    Link: <http://hostname/api/rest/latest/desk/branches?limit=25&page=1>; rel="last"
    X-Total: 3
    
The user can specify whether he wants to get to the **next**, **previous**, **fist** or **last** (as shown in the example above) page in the header. 

### Sorting

The results can be sorted according to the **sort** and **order** parameters. The **sort** parameter performs the sorting according to the property name of an entity, **order** parameter may be set either to **asc** (ascending) or **desc** (descending).

### Filtering

Filtering can be performed according to any parameter of the corresponding entity. For example, to filter the branch by its key, add "key=PO" parameter to the URL.
 
If the value is specified for string property, the search is performed for any occurrence, meaning the result will return PO, DPO, DPOD, etc. If the value is specified for numeric property the search is performed for equal value.

## Error Handling

When the fault occurs within the application or on a server side, the server returns the corresponding status code followed by the message, indicating the root cause in the response body.

Here are the status codes of the errors that may occur when working with DiamanteDesk application.

**400** error indicates that validation failed and the request provided by client was incorrect or distorted and the server could not understand it.

**401** error occurs when a user attempts to access a page or resource that requires authentication. To resolve this issue, correct log in details shall be provided.

**403** error indicates authorization issue, meaning that a user has not been granted permission to access specific page or method.

**404** error means that the server could not process client request with the reason for that described in the error message.

**500** - Internal server error. This status code indicates that this is not a client-side issue, meaning that the problem occurred on the server side rather than in DiamanteDesk application. 

Take a look at the example of a 404 error below:

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

## Resources

REST APIs are necessary when DiamanteDesk is integrated into another application and when interactions with the DiamanteDesk server shall be scripted.

>NOTE: Here are the values of the variables API methods:
>
>|Variable|       Requirements          
|:------------- |:---------------| 
|   {version}   | latest, v1 |
|{_format} | xml, json |

### Branches

###### POST: Create a new branch

    POST /api/rest/{version}/desk/branches
    
**Parameters**

| Name  | Type  | Description |
|:------------- |:---------------|:-------------|
| _name_     | ____ | **Required.** Specify the name of a new branch. |
| _description_     | ____        | Enter the description of a new branch, if necessary. |
| _tags_ | ____       | Specify the tags appropriate for the new branch. To learn more about tagging in DiamanteDesk, please check the **Tagging** section in the **User Guide** section. |
| _key_ | ____ | Enter the key of a new branch. Note that the key should be unique accross the whole system. Branch key must contain only letters. Minimum length is 2 letters.

_Request example:_ 

    {
      "name": "Test Branch",
      "description": "Test Description",
      "tags": [
           "Test Tag"
      ],
      "key": "BRANCHTEST"
    }
    
**Response**
    
**Status Code:** 201 (Created)

_Response body:_ 

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

###### GET: Retrieve the list of all branches

    GET /api/rest/{version}/desk/branches
    
**Response**
    
**Status Code:** 200 (OK)

_Response body:_ 

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
 **Status Code:** 404 (Not Found)

_Response body:_ 

    {
       "error": "Branch loading failed. Branch not found."
    }


######  GET: Retrieve a branch by ID

    GET /api/rest/{version}/desk/branches/{id}
    
**Response**
    
**Status Code:** 200 (OK)

_Response body:_ 

    {
       "created_at": "2015-07-17T11:25:36+0000",
       "description": "Test Description",
       "id": 11,
       "key": "BRANCHTEST",
       "name": "Test Branch",
       "updated_at": "2015-07-17T11:25:36+0000"
    }

###### PUT, PATCH: Update properties of a certain branch

    PUT|PATCH /api/rest/{version}/desk/branches/{id}
    
_Request example:_ 

    {
       "name": "Test Branch PUT",
       "description": "Test Description",
       "tags": [
           "Test Tag"
       ]
    }
    
**Response**
    
**Status Code:** 200 (OK)

_Response body:_ 

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


###### DELETE: Delete a branch by ID

    DELETE /api/rest/{version}/desk/branches/{id}
    
**Response**
    
**Status Code:** 204 (No Content)

_Response body:_ null

### Tickets

###### POST: Create a new ticket

    POST /api/rest/{version}/desk/tickets
    
| Name  | Type  | Description |
|:------------- |:---------------|:-------------|
| branch     | ____ | **Required.** Specify a branch where the ticket should be created.
| subject     | ____        | **Required.** | Enter the short description of a new ticket.
| description | ____       | **Required.** Enter the description of a new ticket.
| status | ____ |**Required.** The available statuses are: **New**, **Open**, **Pending**, **In progress**, **Closed** and **On Hold**.
| priority | ____ |**Required.** Specify the priority of a new ticket. The available options are **Low**, **Medium** or **High**.
| source | ____ |**Required.** Every service user has 4 available options to contact the Help Desk team: by creating a request through a **Web** form or through the embedded form on a website (optional), as an **Email** notification, via a **Phone** call. Specify the corresponding source of a ticket.
| reporter| ____ |**Required.** The reporter is an administrator who can create a ticket for any customer.
    
_Request example:_

    {
       "branch": 1,
       "subject": "Test Ticket",
       "description": "Test Description",
       "status": "open",
       "priority": "medium",
       "source": "phone",
       "reporter": "diamante_10"
    }
**Response**
    
**Status Code:** 201 (Created)

_Response body:_ 

    {
       "attachments": [

       ],
       "branch": 1,
       "comments": [

       ],
       "created_at": "2015-07-17T11:25:29+0000",
       "description": "Test Description",
       "id": 11,
       "key": "BRANCHB-2",
       "priority": "medium",
       "reporter": "diamante_10",
       "source": "phone",
       "status": "open",
       "subject": "Test Ticket",
       "unique_id": {
           "id": "80297640927352a82f2b7c1a8c97d10b"
       },
       "updated_at": "2015-07-17T11:25:29+0000"
    }

###### GET: Retrieve list of all Tickets

    GET /api/rest/{version}/desk/tickets

**Response**
    
**Status Code:** 200 (OK)

_Response body:_ 

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

###### GET: Retrieve ticket by the given ticket ID

   GET /api/rest/{version}/desk/tickets/{id}
   
**Response**
    
**Status Code:** 200 (OK)

_Response body:_ 

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

###### PUT, PATCH: Update certain properties of the ticket by ID

    PUT, PATCH /api/rest/{version}/desk/tickets/{id}
    
_Request example:_

    {
       "subject": "Test Ticket Updated PUT"
    }
    
**Response**
    
**Status Code:** 200 (OK)

_Response body:_ 

    {
       "attachments": [

       ],
       "branch": 1,
       "comments": [

       ],
       "created_at": "2015-07-17T11:25:29+0000",
       "description": "Test Description",
       "id": 11,
       "key": "BRANCHB-2",
       "priority": "medium",
       "reporter": "oro_1",
       "source": "phone",
       "status": "open",
       "subject": "Test Ticket Updated PUT",
       "unique_id": {
           "id": "4b1573586e00d7760babf2aa0bdb9cdc"
       },
       "updated_at": "2015-07-17T11:25:47+0000"
    }
    
###### DELETE: Delete the ticket by ID

    DELETE /api/rest/{version}/desk/tickets/{id}   
    
**Response**

**Status Code:** 204 (No Content)

_Response body:_ null
    
**Status Code:** 404 (OK)

_Response body:_   

    {
    "error": "Ticket loading failed, ticket not found."
    }   
    
    
###### GET: Retrieve ticket by the given ticket key

   GET /api/rest/{version}/desk/tickets/{key}
   
**Response**
    
**Status Code:** 200 (OK)

_Response body:_ 

    {
       "attachments": [

       ],
       "branch": 1,
       "comments": [

       ],
       "created_at": "2015-07-17T11:25:29+0000",
       "description": "Test Description",
       "id": 11,
       "key": "BRANCHB-2",
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

###### PUT, PATCH: Updates certain properties of the ticket by the key

    PUT, PATCH /api/rest/{version}/desk/tickets/{key}
    
_Request example:_

    {
       "subject": "Test Ticket Updated PUT by key"
    }
    
**Response**
    
**Status Code:** 200 (OK)

_Response body:_ 

    {
       "attachments": [

       ],
       "branch": 1,
       "comments": [

       ],
       "created_at": "2015-07-17T11:25:29+0000",
       "description": "Test Description",
       "id": 11,
       "key": "BRANCHB-2",
       "priority": "medium",
       "reporter": "diamante_10",
       "source": "phone",
       "status": "open",
       "subject": "Test Ticket Updated PUT by key",
       "unique_id": {
           "id": "80297640927352a82f2b7c1a8c97d10b"
       },
       "updated_at": "2015-07-17T11:25:29+0000"
    }
    
###### DELETE: Deletes the ticket by the key

    DELETE /api/rest/{version}/desk/tickets/{key} 
    
**Response**

**Status Code:** 204 (No Content)

_Response body:_ null
    
**Status Code:** 404 (OK)

_Response body:_   

    {
    "error": "Ticket loading failed, ticket not found."
    }   

###### /api/rest/{version}/desk/tickets/search

|Method|        Description          
|:------------- |:---------------| 
| **GET**    | Retrieves list of Tickets found by the query. Ticket is searched by the subject and description. Performs filtering of tickets if provided with criteria as GET parameters. Time filtering parameters as well as paging/sorting configuration parameters can be found in \Diamante\DeskBundle\Api\Command\Filter\CommonFilterCommand class. Time filtering values should be converted to UTC.|

###### GET: Retrieves the list of ticket attachments by ticket ID

    GET /api/rest/{version}/desk/tickets/{id}/attachments
    
**Response**
    
**Status Code:** 200 (OK)

_Response body:_ 
    
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

###### GET: Retrieve personal data based on the provided ID

    GET /api/rest/{version}/desk/ticket/{id}/assignee

**Response**
    
**Status Code:** 201 (Created)

_Response body:_ 

    {
       "email": "pol.vova@gmail.com",
       "name": "asdasd dasdasd",
       "id": "oro_1"
    }


###### POST: Add attachment to the ticket

    POST /api/rest/{version}/desk/tickets/{ticketId}/attachments

_Request example:_

    {
       "attachmentsInput": [
           { 
       BASE_64 encoded file
           }
       ]
    }
    
**Response**
    
**Status Code:** 201 (Created)

_Response body:_ 

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

###### GET: Retrieve ticket attachment by attachment ID

    GET /api/rest/{version}/desk/tickets/{ticketId}/attachments/{attachmentId}
    
**Response**
    
**Status Code:** 200 (OK)

_Response body:_ 

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
    
###### DELETE: Remove Attachment from the ticket

    DELETE /api/rest/{version}/desk/tickets/{ticketId}/attachments/{attachmentId}
    
**Response**
    
**Status Code:** 204 (No Content)

_Response body:_ null

**Status Code:** 404 (Not Found)

_Response body:_

    {
       "error": "Attachment loading failed. Ticket has no such attachment."
    }

### Comments

###### POST: Posts a new comment to the ticket.

    POST /api/rest/{version}/desk/comments
    
    
| Name  | Type  | Description |
|:------------- |:---------------|:-------------|
| content     | ____ | **Required.** Add your comment into this section. |
| ticket     | ____        | _______ |
| author | ____       | Specify the user who adds the comment to the ticket. |
| ticketStatus | ____ | **Required.** The available statuses are: **New**, **Open**, **Pending**, **In progress**, **Closed** and **On Hold**.
    
_Request example:_

    {
       "content": "Test Comment",
       "ticket": 1,
       "author": "diamante_10",
       "ticketStatus": "new"
    }   

    
**Response**
    
**Status Code:** 201 (Created)

_Response body:_ 

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

###### GET: Retrieve the list of all comments

    GET /api/rest/{version}/desk/comments
    
**Response**
    
**Status Code:** 200 (OK)

_Response body:_ 

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

###### GET: Retrieve the comment by the given comment ID

    GET /api/rest/{version}/desk/comments/{id}
        
**Response**
    
**Status Code:** 200 (OK)

_Response body:_ 

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
    
###### PUT, PATCH: Update certain properties of the comment be the comment ID.

    PUT|PATCH /api/rest/{version}/desk/comments/{id}
    
**Response**
    
**Status Code:** 200 (OK)

_Request example:_

    {
       "content": "Test Comment Updated PUT",
       "ticketStatus": "closed"
    }

_Response body:_ 

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

###### DELETE: Delete a ticket comment by the comment ID

    DELETE /api/rest/{version}/desk/comments/{id}
    
**Response**

**Status Code:** 204 (No Content)

_Response body:_ null
    
**Status Code:** 404 (OK)

_Response body:_   

    {
    "error": "Comment loading failed, comment not found."
    }  

###### GET: Retrieve comment author information based on the provided ID

    GET /api/rest/{version}/desk/comment/{id}/author

**Response**
    
**Status Code:** 200 (OK)

_Response body:_

    {
       "email": "pol.vova@gmail.com",
       "name": "asdasd dasdasd",
       "id": "oro_1"
    }

###### GET: Retrieves comment attachments

    GET /api/rest/{version}/desk/comments/{id}/attachments

**Response**
    
**Status Code:** 200 (OK)

_Response body:_

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


###### POST: Add attachments to the comment

    POST /api/rest/{version}/desk/comments/{commentId}/attachments

_Request example:_

    {
       "attachmentsInput": [
           { 
       BASE_64 encoded file
           }
       ]
    }
    
**Response**
    
**Status Code:** 201 (Created)

_Response body:_

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

###### Retrieve the comment attachment by the attachment ID

    GET /api/rest/{version}/desk/comments/{commentId}/attachments/{attachmentId}
    
**Response**
    
**Status Code:** 200 (OK)

_Response body:_

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

######  Remove the attachment from the comment by the attachment ID

    DELETE /api/rest/{version}/desk/comments/{commentId}/attachments/{attachmentId}
    
**Response**

**Status Code:** 204 (No Content)

_Response body:_ null
    
**Status Code:** 404 (OK)

_Response body:_   

    {
    "error": "Attachment loading failed. Comment has no such attachment."
    } 

### Users

###### POST: Create a new user

    GET /api/rest/{version}/desk/users
    
**Parameters**

| Name  | Type  | Description |
|:------------- |:---------------|:-------------|
| firstName     | ____ | **Required.** Provide the first name of a new user. |
| lastName     | ____        | **Required.** Provide the last name of a new user.|
| email | ____       | **Required.** Add an email of e new user. This email is going to be used for email notifications and password recovery.|
    
_Request example:_

    {
       "email": "1437135532dummy-test-email-address@test-server.local",
       "firstName": "John",
       "lastName": "Dou"
     }
**Response**
    
**Status Code:** 201 (Created)

_Response body:_

    {
       "id": 11,
       "email": "1437135532dummy-test-email-address@test-server.local",
       "first_name": "John",
       "last_name": "Dou"
    }
    
###### GET: Retrieve the list of all DiamanteDesk users

    GET /api/rest/{version}/desk/users
    
**Response**
    
**Status Code:** 200 (OK)

_Response body:_

     [
         {
            "id": 10,
            "email": "test1@test.com",
            "first_name": "Test",
            "last_name": "test"
         },
         {
            "id": 11,
            "email": "1437135532dummy-test-email-address@test-server.local",
            "first_name": "John",
            "last_name": "Dou"
         }
    ]


###### GET: Retrieve DiamanteDesk user data

    GET /api/rest/{version}/desk/users/{email}/
    
**Response**
    
**Status Code:** 200 (OK)

_Response body:_

    {
       "id": 11,
       "email": "1437135532dummy-test-email-address@test-server.local",
       "first_name": "John",
       "last_name": "Dou"
    }

**Status Code:** 404 (Not Found)

_Response body:_

    {
       "error": "User not found."
    }