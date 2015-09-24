---
title: Data Audit
---

Every time a customer or administrator performs any action in the system, this action is added to the read-only event-action history log. Actions are entity properties that are created, updated or removed. Entities are users, branches, tickets, comments, attachments. Examples of actions stored in the action history log:

* A new user was created in the system
* A new comment was added
* An existing ticket was updated
* A branch was deleted

To view all the actions made by the users in the system, move to _System > Data Audit_. The **Data Audit** screen opens. This screen contains the following information regarding the actions performed:


Field  | Description
------------- | -------------
Action  | This field defines the action performed by a user. The available actions are: **Update**, **Create**, **Delete**.
Version | Current field indicates how many actions has been created to this entity. For example, 
Entity Type | This field indicates the entity type modified by a DiamanteDesk user. This can be any of the following entity types: **User**, **Branch**, **Ticket**, **Comment**, **Attachment**.
Entity Name | This field contains the name of a user, branch, ticket, comment or attachment.
Entity ID | Entity ID is a unique number of an entity in the system.
Data | All the data added to the entity where the action is performed is indicated in this field. For example, when a new ticket is created, the **Data** field contains such information as ticket subject, description, status, priority, reporter and the branch.
Author | The name of a person who performed current changes in the system is indicated in this field.
Organization | This field indicates an organization specified during DiamanteDesk or OroCRM installation.
Logged at | The date and time when the action is performed is shown in this field.

_**Note:** You can filter the data audit information according to the following criteria:_

* _Action_
* _Entity Type_
* _Entity Name_
* _Entity ID_
* _Author_