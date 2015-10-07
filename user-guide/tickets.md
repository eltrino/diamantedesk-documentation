---
title: Tickets
---

DiamanteDesk is a great way to improve customer experience by easily receiving, reassigning and taking care of any Client requests presented as **tickets**.

Tickets in DiamanteDesk can be created through one of the following channels:

* through the [**web portal**](channels/portal.md);
* via [**embedded forms**](embedded-form.md) on websites, online stores, blogs, etc.;
* via [**processing email requests**](email-processing.md) sent to the support email address;
* by the admin users via the admin panel.

Tickets in the admin panel can be viewe
d and created at:

* the **Branches** top menu (see [**Branches**](branches.html) section);
* the **All Tickets** top menu.

![All tickets](img/All_tickets.png)

<a name="create-a-new-ticket"></a>
## Create a New Ticket

To create a new ticket, complete the following steps:

Click **Create Ticket** at the top right corner of the screen. The **Create Ticket** screen opens.

![Create ticket](img/create_ticket_1.1.png)

Provide all the relevant information necessary to create a new ticket:

Field  | Description
------------- | -------------
Branch  | Click the down arrow to choose a branch where this ticket is going to be created.
Subject | Briefly describe the substance of the issue in this field.
Status | Select the status of a ticket. The available statuses are **New**, **Open**, **Pending**, **In Progress**, **Closed** and **On Hold**. When the ticket is just created, its status is normally set to **New** or **Open**.
Priority | Set the priority of the ticket according to urgency and severity of the issue occurred. The available priority options are **Low**, **Medium** or **High**.
Source | Specify the channel used to submit this ticket. The available options are: through **Web**, **Phone** or **Email**. To learn more about channels of ticket submitting, follow this [link](channels/index.md).
Reporter | Reporter is a user who created a ticket or who is in charge if it. This user receives notifications whenever the ticket status or priority changes. By default, the reporter is an owner of the account where the user is currently logged in. To change the reporter, click the list button and select the corresponding user.
Assignee | Assignee is a person responsible for the ticket workflow. To change the reporter, click the list button and select the corresponding user.
File | In case there is a file that shall be attached to the ticket (screenshot or document), click **Choose file** and select the required file from your local machine.
Tags | Add tags for the further quick ticket search and classification. Follow the link to learn more about [tagging](tagging.md) in DiamanteDesk.

Provide the detailed description of a ticket in the **Description** field. If relevant, describe the steps to reproduce the bug/error.

![Create ticket](img/description_field.png)

Click **Save** or **Save and Close** at the right top corner of the screen for a corresponding action.

## Ticket Comments

Once the ticket is created and successfully saved in the system, customers can comment them from the portal and admin users can add comments to them from the admin panel either publically or privately.

**Comments on the Portal**

Whenever DiamanteDesk customer needs to add more information about the issue or make a request about the previously created ticket, the comment to this ticket can be added on the portal. 

![Comments](img/comments_portal.png)

This comment automatically becomes available at the admin panel, updating admin users with new information/requests/issues occurred.

**Comments on the Admin Panel**

To add a comment to some ticket at the DiamanteDesk admin panel, open the required ticked and click the **Comment** button at the **Comments** section. The **Add Comment** screen opens.

![Comments](img/comments_backend.png)

Field  | Description
------------- | -------------
Content  | This field contains the comment body.
Ticket Status  | Specify whether the ticket status has changed. Once comment with the changed ticket status is added, the status of the ticket automatically changes as well.
Attachments  | Attach screenshots clarifying or confirming information provided in the content field.
Private  | If this checkbox is selected, this comment is going to be available only to the admin users on the DiamanteDesk admin panel. If the checkbox is clear, it s going to be available both for admin users on the admin panel and for the customer on the portal.

## Notifications

**Email Notifications** is a DiamantDesk feature that sends automatic emails to the ticket creator and assignee when the ticket is created or its [status](#status) changes. This way a customer is notified whether his request is being processed.

When the ticket is created, a reporter and assignee get the following emails, informing them about ticket branch, subject, priority, status and source:

![Notifications](img/status_email.png)

When the status of a ticket changes, the reporter and assignee get the following email, informing them about changes performed and the person responsible for them:

![Notifications](img/status_email_2.png)

### Configuring Notifications

This functionality can be configured according to the customer needs at _System > Configuration_. On the left side side of the screen on the **System configuration** pane select **Notifications** tab in the **DiamanteDesk** menu.

![System configuration](img/sys_config.jpg)

**Notifications** tab opens.

![Notifications](img/notifications.png)

To use the default settings, select the **Use Default** check box in the **Email Notifications** field. 

To edit the configurations, clear the the **Use Default** check box and set the **Enable Email Notifications** field to **Yes** or **No** option.

To save the changes made, click **Save Settings** on the left top corner of the screen.

### Server Setup

The mailer settings for emails and notifications are usually configured during DiamanteDesk installation. To learn more about the process of installation, navigate to the Installation Guide section of the documentation.

![Notifications](img/web_config.png)

To make sure that server parameters are configured correctly or you need to change them, define required configuration details in the **app/config/parameters.yml** file. If you need more information on how to perform configurations in the **app/config/parameters.yml** file, follow this [link](https://symfony.com/doc/current/best_practices/configuration.html).

## Watchers

Each of the tickets can be assigned to a specific user to make sure that a given issue is solved quickly and efficiently. But in order to have more control over certain high priority issues, a new **Watchers** feature has been added.

A **Watcher** is a person who gets an email notification every time a status, priority or other valuable ticket information changes. When the ticket is created, a **Reporter** (the person who created a ticket) and an **Assignee** (a person to whom the ticket is assigned) automatically become **Watchers**. If the ticket is created by the admin user, he automatically becomes a ticket watcher as well.

###Adding Watchers to the Ticket

Watchers can be added to the ticket in one of the following ways:

* **By the Customer via Email**

In case the ticket is created from the email through [email processing](email-processing.md), the email sender and all the users from CC (if any) become watchers and receive email notifications each time the ticket content, status or priority changes.

* **By the Customer via the Portal**

To add watchers to the ticket via the portal, complete the following steps:

1. Log into the Portal.
2. Create a new ticket. To get the detailed instructions on how to create ticket via the portal, please refer to [this section](#create-a-new-ticket).
3. Once the ticket is submitted, the screen with ticket description and editing options is opened. At the right side of this screen in the **Watchers** section click **Add Watcher** to add a person or several people who will be able to control the ticket workflow.
![Create ticket](img/ticket_submitted.png)
4. The **Add Watcher** screen opens. Specify the email of a person you would like to make a watcher for this ticket and click **Add**. If this email has been previously registered in DiamanteDesk, the system will automatically define this user and will add the person's first an last name to the list of watchers. If no matching account has been found a new DiamanteDesk customer is created.
![Create ticket](img/add_watcher_portal.png)
5. An email confirmation is sent to a person whose email was provided at the **Add Watcher** screen, notifying him on the new role granted.

* **By the Admin User via Admin Panel**

Admin user can add or remove certain users from the list of ticket watchers if this administrator has the corresponding edit permissions. To follow the changes made in a certain ticket or add other customers/administrators to the list of watchers, admin user should perform the following steps:

1. Log into the DiamanteDesk admin panel.
2. Open the required ticket either at _Desk > Branches > select a branch_ or at _Desk > All Tickets_.
3. To to be aware of the changes made to the ticket, click **Watch** on the option panel at the top of the screen. 
![Create ticket](img/add_watcher_admin.png)
To add another person to the **Watchers** list, click **Add Watcher** on the option panel. The **Add Watcher** screen opens. Enter the name of a required user or click a list button and select a user from the list of available users.