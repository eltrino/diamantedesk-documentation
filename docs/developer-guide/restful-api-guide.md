#RESTful API Guide

This section describes WSSE authentication mechanism and DiamanteDesk REST API resources.

## Authentication

DiamanteDesk uses [WSSE authentication](https://en.wikipedia.org/wiki/WS-Security) to ensure secure access to the third party applications via REST APIs. WSSE authentication in DiamanteDesk application, which is based on Symfony, is implemented by using this [bundle](https://github.com/escapestudios/EscapeWSSEAuthenticationBundle).

WSSE authentication is based on:

* a username;
* a nonce (a cryptographic number generated to prevent replay attacks);
* current timestamp;
* the password digest (In DidamanteDesk the password digest is represented as API Key. To learn how to generate API key, please see the **API Credentials** article in the **Integration** section of DiamanteDesk documentation).


## DiamanteDesk API Resources

REST APIs are necessary when DiamanteDesk is integrated into another application and when interactions with the DiamanteDesk server shall be scripted.

>NOTE: Here are the values of the variables API methods:
>
>|Variable|       Requirements          
|:------------- |:---------------| 
|   {version}   | latest, v1 |
| {id}    | \d+  |
|{_format} | xml, json |

### Branches

###### /api/rest/{version}/desk/branches



|Method |  Description               
|:------------- |:---------------| 
| **GET**    |  Retrieves the list of all Branches. Filters branches with parameters provided within GET request. Time filtering parameters as well as paging/sorting configuration parameters can be found at \Diamante\DeskBundle\Api\Command\CommonFilterCommand class. Time filtering values should be converted to UTC. |
| **POST**    | Creates a new branch.  |

###### /api/rest/{version}/desk/branches/{id}
|Method|        Description          
|:------------- |:---------------| 
| **GET**    | Retrieves a branch by ID. |
| **PUT**, **PATCH**    | Updates certain properties of the branch. |
| **DELETE** | Deletes a branch. |

### Tickets

###### /api/rest/{version}/desk/tickets

|Method|        Description          
|:------------- |:---------------| 
| **GET**    | Retrieves list of all Tickets. Performs filtering of tickets if provided with criteria as GET parameters. Time filtering parameters as well as paging/sorting configuration parameters can be found in \Diamante\DeskBundle\Api\Command\Filter\CommonFilterCommand class. Time filtering values should be converted to UTC.|
| **POST** | Create a new ticket.|

###### /api/rest/{version}/desk/tickets/{id}

|Method|        Description          
|:------------- |:---------------| 
| **GET**    | Loads a ticket by the given ticket ID. |
| **PUT**, **PATCH**    | Updates certain properties of the ticket. |
| **DELETE** | Deletes the ticket by ID. |

###### /api/rest/{version}/desk/tickets/{key}

|Method|        Description          
|:------------- |:---------------| 
| **GET**    | Loads a ticket by the given ticket key. |
| **PUT**,**PATCH**    | Updates certain properties of the Ticket by its key. |
| **DELETE** | Deletes Ticket by key |

###### /api/rest/{version}/desk/tickets/search

|Method|        Description          
|:------------- |:---------------| 
| **GET**    | Retrieves list of Tickets found by the query. Ticket is searched by the subject and description. Performs filtering of tickets if provided with criteria as GET parameters. Time filtering parameters as well as paging/sorting configuration parameters can be found in \Diamante\DeskBundle\Api\Command\Filter\CommonFilterCommand class. Time filtering values should be converted to UTC.|

###### /api/rest/{version}/desk/tickets/{id}/attachments

|Method|        Description          
|:------------- |:---------------| 
| **GET**    |  Lists ticket attachments. |

###### /api/rest/{version}/desk/ticket/{id}/assignee

|Method|        Description          
|:------------- |:---------------| 
| **GET**    |  Retrieves personal data (of a provider or assignee) based on the provided ID.|

###### /api/rest/{version}/desk/tickets/{ticketId}/attachments

|Method|        Description          
|:------------- |:---------------| 
| **POST**    |  Adds attachments for ticket. |

###### /api/rest/{version}/desk/tickets/{ticketId}/attachments/{attachmentId}

|Method|        Description          
|:------------- |:---------------| 
| **GET**    | Retrieves ticket attachment. |
| **DELETE** | Removes Attachment from Ticket|

### Comments

###### /api/rest/{version}/desk/comments

|Method|        Description          
|:------------- |:---------------| 
| **GET**    | Retrieves list of all Comments. Filters comments with parameters provided via GET request. Time filtering parameters as well as paging/sorting configuration parameters can be found in \Diamante\DeskBundle\Api\Command\CommonFilterCommand class. Time filtering values should be converted to UTC. |
| **POST**    | Posts a new comment to the ticket. |

###### /api/rest/{version}/desk/comments/{id}

|Method|        Description          
|:------------- |:---------------| 
| **GET**    | Loads comment by the given comment ID. |
| **PUT**, **PATCH**    | Updates certain properties of the comment. |
| **DELETE** | Deletes a ticket comment. |

###### /api/rest/{version}/desk/comment/{id}/author

|Method|        Description          
|:------------- |:---------------| 
| **GET**    | Retrieves comment author data based on the provided ID. |

###### /api/rest/{version}/desk/comments/{id}/attachments

**GET**

|Method|        Description          
|:------------- |:---------------| 
| **GET**    | Retrieves comment attachments. |

###### /api/rest/{version}/desk/comments/{commentId}/attachments

|Method|        Description          
|:------------- |:---------------| 
| **POST**    | Adds attachments to the comment. |

###### /api/rest/{version}/desk/comments/{commentId}/attachments/{attachmentId}

|Method|        Description          
|:------------- |:---------------| 
| **GET**    | Retrieves comment attachment. |
| **DELETE** | Removes attachment from the comment. |

### Users

###### /api/rest/{version}/desk/users

|Method|        Description          
|:------------- |:---------------| 
| **GET**    | Retrieves all DiamanteDesk Users.|
| **POST**    |  Creates a new DiamanteDesk user. |


###### /api/rest/{version}/desk/users/{email}/

|Method|        Description          
|:------------- |:---------------| 
| **GET**    | Retrieves DiamanteUser data if one exists. |
