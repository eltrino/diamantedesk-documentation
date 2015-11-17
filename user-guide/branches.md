---
title: Branches
---

When a customer of any web service supported by the DiamanteDesk needs to report an issue or submit a request to the help desk team, a _ticket_ is created. Each ticket in DiamanteDesk application has a unique identificator and is sorted according to the _branch_ where it is created or is added to a default branch.

Creating separate branches in DiamanteDesk enables our Clients to group tickets according to the requests of specific users, locations, issues or according to the [Channel](channels/index.html) the ticket came from. Branch logic helps to organize tickets in a way to keep track of the tickets according to a certain category and quickly find them in a system. We remember that good customer service implies quick reaction and problem solving, so we do our best to provide our Clients with a user-friendly tool to make it work.

_**Note:** When the ticket is automatically created from the email received at the the support email address, this ticket is created at the branch which is configured as a default one. To learn more about it, please see the [Email Processing](channels/email-processing.html) section._

To see the list of all available branches, select the **Branches** tab at the navigation panel at the top of the home screen. 

![Branches](img/branches.png)

## Branch Filters

All branches can be filtered according to the **Branch Name** or **Branch Key**. 

Branch key is automatically generated from the branch name when a new branch is created and it should be unique across the system. Branch key must contain only letters. Minimum length is 2 letters. If Branch name consists of more than one word, the system takes the first character of every word and converts them to upper case (for example, Green Daisy - GD, Diamante Desk - DD, etc.). If branch name consists of a single word, branch key is generated from the first 2-4 characters in the upper case (for example, Eltrino - ELTR, bbq - BBQ, etc.).

**Branch name** and **Branch Key** filters are set to **All** values by default. To filter the branches according to a certain branch name or key, click the down arrow in the corresponding filed and enter the required name or key. To refresh the results, click **Refresh**. To clear all filters, click **Reset**.

To learn more about filtering in DiamanteDesk, follow this [link](filtering.html).

## Create a New Branch

Click **Create** at the right top corner of the **Branches** screen. **Create Branches** screen opens.
![Create branch](img/create_branches_details.png)

Provide the required information into each field. Not all the fields are required, but the more data you provide, the easier it is to distribute the tickets into the corresponding fields and finding them when they are needed:

Field  | Description
:------------- | -------------
Name  | _Required._ Provide the name of a new branch in this field.
Key | Leave a **Key** field empty as it is automatically filled by the system. Branch Key is generated from the branch name and it should be unique across the system.
Default Assignee | To select the **Assignee**, click **Unassigned**. A Search Panel opens. Next, the following two options are available: you can either start entering the name of the person to be assigned and the system will provide hints with matching results or you can click a list image to open a list of all available assignees. _**Note:** If you have selected a wrong assignee, click the X button next to the name of an assignee._
Image |Add an image that will serve as a branch logo to the **Image** field. To do that, click **Choose file** and select a required image from your local machine.
Tags | You can also tag your branch. Follow the link to learn more about [branch tagging](tagging.html).

Provide the description of the branch in the **Description** filed.

![Create branch](img/create_branches_description.png)

Provide the support email address matching this branch in the **Support Address** field (for example, it is a good idea to add all the tickets sent to sales@companyname.com to the "Sales" branch) and the customer domain name (for example, eltrino.com) to add all the emails sent from the email addresses with such customer domain to a specific branch.

![Email configuration](img/email_config.png)

Click [here](channels/email-processing.html) if you want to learn more about email processing in DiamanteDesk.

Click **Save And Close** at the right top corner of the screen.

## Edit a Branch

1. Navigate to the **Branches** screen.
2. Select the branch that shall be edited from the list of available branches. The selected **Branch** screen opens.
3. Click **Edit** at the right top corner of the screen:
![Branch Edit Delete](img/branches_edit.png)
4. Perform the necassary changes/updates.
5. Click **Save** or **Save and Close** for the corresponding action.

## Delete a Branch

Three options of branch deleting are available in DiamanteDesk.

### Deleting a Single Branch

When attempting to delete a single branch in DiamanteDesk, keep in mind that ALL its tickets are going to be deleted as well.

1. Navigate to the **Branches** screen.
2. Select the branch that shall be deleted from the list of available branches. The selected **Branch** screen opens.
3. Click **Delete** at the right top corner of the screen:
![Branch Delete](img/branches_delete1.png)
_**Note:** When attempting to delete a single branch in DiamanteDesk, keep in mind that ALL its tickets are going to be deleted as well._
4. The following confirmation message appears:
SCREEN
5. To delete a branch but keep all the tickets in the system, select a corresponding checkbox in the warning message and choose a new branch where all the tickets shall be moved from the drop-down as shown on the picture below:
SCREEN

_**Note:** If a branch is configured as default for [Email Processing](channels/email-processing.html), it cannot be deleted and the following message is displayed at the top of the **Branch** screen:_
![Default Branch](img/branches_default.png)

### Branch Deleting Mass Action 

Multiple branches can be deleted via mass action functionality in DiamanteDesk. Perform the folllowing steps in order to delete several branches at once:

1. Navigate to the **Branches** screen.
2. Select several branches that shall be deleted from the list of available branches. 
3. Click the **Mass Actions** button and select the **Delete Branches** option as shown on the picture below.
![Branches](img/branches_mass_action.png)
4. The **Delete Confirmation** message opens.
![Branches](img/delete_confirmation.png)
5. Click **Yes, Delete** to proceed woth deleting and **Cancel** to retern to the **Branches** screen. _Please note that a branch cannot be deleted via mass action if it has any tickets. Only the branches without any tickets can be deleted during branch deleting mass action._

### Deleting Branches through API

Branches can also be deleted via the corresponding APIs. The DiamanteDesk RESTful API guide is available [here](../developer-guide/restful-api-guide.md).

_Please note that a branch cannot be deleted via API request if it has any tickets. Only the branches without any tickets can be deleted via API request._