---
title: Rules
---

**Rules** in DiamanteDesk allow configuring automatic system behaviour according to certain scenarios and conditions without having to request developers help. For example, when a new ticket is created via email processing, portal or from the admin panel and the **Subject** field contains "ASAP" acronym or other specific word or phrase that implies some sort of urgency, the priority of a ticket is automatically set to **High** in order to make sure it will be quickly taken care of.

The ability to create rules garantees flexible approach and easy system configuration whenever specicific needs and requirements arise.

This article covers basic working principles related to business and automation rules in DiamanteDesk.

## Create a New Automation Rule

To create a new rule:

1. Go to _Desk > Business Rules_.
2. Click _Create_ to add a new rule to the system behaviour scenario. The _New Rule_ screen opens.
3. Provide a unique name for a new rule in the _Name_ field of the _General_ section of the screen.
4. Select the condition or a group of conditions when this rule should be applied. Detailed description of conditions is provided in the [following section](#conditions) of this article.
5. After a condition or a group of conditions is specified in the **Conditions** section, determine the action that shall be further performed by the system. Click **New Action**. Select the corresponding action from the drop-down list. Now each time this condition or a group of condition criteria is met, this action is automatically performed by the system.
6. Click **Save** or **Save and Close** for the corresponding action.

<a name="conditions"></a>
### Conditions

Specify the criteria which shall determine specific system behaviour in the **Conditions** section. The criteria may be added as:

* **a single condition.** Click **New Condition** to specify one. Select the condition from the drop-down list.
* **a logical group of conditions.** In some cases a specific action shall be performed when several condition criteria are met at once or when any of the specified criteria is met. For example, when a ticket has an attachment and its status is set to **High**, an email notification shall be automatically sent to a specified admin user. Click **New Group**. Select several conditions from the drop-down list. Select whether **All** or **Any** of the condition criteria should be met for the action to be performed. _**Note:** Several logical groups may be created. You can drag and drop any condition criterion to move it form one group to another._
