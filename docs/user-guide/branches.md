#Branches

When a customer of any service which is supported by the DiamanteDesk needs to report an issue or add a request, he creates a ticket. Each ticket has a unique identificator and is sorted according to the Branch where it is created or is added to a default branch.

Branches allow grouping tickets related to a certain customer or user.

_Note:_ When the ticket is automatically created from the email received at the the support email address, this ticket is created at the branch which is configured as a default one. Default branch cannot be deleted. 

To see the list of all available branches, go to **Desk > Branches**. 

![Branches](img/branches.png)

All branches can be filtered according to the **Branch Name** or **Branch Key**. 

Branch key is automatically generated from the branch name when a new branch is created and it should be unique across the system. Branch key must contain only letters. Minimum length is 2 letters. If Branch name consists of more than one word, the system takes the first character of every word and converts them to upper case (for example, Green Daisy - GD, Diamante Desk - DD, etc.). If branch name consists of a single word, branch key is generated from the first 2-4 characters in the upper case (for example, Eltrino - ELTR, bbq - BBQ, etc.).

**Branch name** and **Branch Key** filters are set to **All** values by default. To filter the branches according to a certain branch name or key, click the down arrow in the corresponding filed and enter the required name or key. To refresh the results, click **Refresh**. To clear all filters, click **Reset**.

To create a new branch:

1. Go to Desk > Branches.
2. Click **Create** at the right top corner of the screen. **Create Branches** screen opens.
![Create branch](img/create_branches.png)
3. _Required field._ Enter the name of a new branch into the **Name** field.
4. Leave a **Key** field empty as it is automatically filled by the system. Branch Key is generated from the branch name and it should be unique across the system.
5. To select the **Assignee**, click **Unassigned**. A Search Panel opens. Nest, two options are available:
   * Start entering the name of the person to be assigned and the system will provide hints with matching results.
   * Click a list image to open a list of all available assignees. 
_Note:_ If you have selected a wrong assignee, click the X button next to the name of an assignee.
6. Add an image that will serve as a branch logo to the **Image** field. To do that, click **Choose file** and select a required image from your local machine.
7. Provide the description of the branch in the **Description** filed.
8. Provide the domain name of the support email account (for example, mail.google.com, mail.outlook.com, etc.) in the **Support Address** field (for example, support@diamantedesk.com) and the specific user address (for example, support@diamantedesk.com) in the **Customer Domain** field.
![Email configuration](img/email_config.png)
9. Click **Save And Close** at the right top corner of the screen.