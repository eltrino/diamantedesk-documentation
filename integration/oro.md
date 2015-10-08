---
title: OroCRM
---

DiamanteDesk is an independent help desk system that can be easily integrated into the open-source OroCRM and in the near future it is going to be available for other CRMs.  Therefore, DiamanteDesk can be installed as a standalone application or as a help desk extension to the OroCRM. To learn how to install DiamanteDesk, please refer to the [Installation Guide](../installation-guide/index.html).

The following guide is based on the assumption that DiamanteDesk is installed on the basis of OroCRM and describes the functionality related to the DiamanteDesk integration with this system.

When installed on the basis of the OroCRM, DiamanteDesk functionality is available at the **Desk** top menu.

![Oro](img/Oro.png)

This menu provides fast and easy access to the general functionality and data of the DiamanteDesk application, specifically:

* [Branches](../user-guide/branches.html)
* [Tickets](../user-guide/tickets.html)
* Reports

## DiamaneteDesk Contacts in OroCRM

In the Oro platform all the contacts related to any business activities are saved at _Customers > Contacts_. Please refer to the Oro [documentation](http://www.orocrm.com/documentation/index/current/user-guide/contacts) to learn more about contacts in OroCRM. Due to the DiamanteDesk integration with Oro, when a customer registers on the support [portal](http://orocrmqa.eltrino.com:8090/diamante_1.1/web/app_dev.php/portal/#login) to make a request or report an issue regarding the supported entity (online store, blog, etc.), the provided credentials are  added both to the DaiamnteDesk and to the OroCRM contacts. To learn how to configure this option, refer to the [**Configuration**](#configuration) section of this article.

When a user registeres on the portal, the system automatically scans the contact database by the existing emails. If none of the emails match the provided credentials, a new contact is created based on the data provided by the user. If an account with the same email has  been previously registered in the system, the following warning message is displayed:

![Message](img/message.png)

The identical procedure occurs when OroCRM administartor creates a new DiamanteDesk user from the admin panel at _Customers > Contacts > Create Customer_.

This feature can be disabled at _System > Configuration > DiamanteDesk_.

## Tickets in OroCRM

When DiamanteDesk is installed on the basis of the OroCRM, administrators can view the tickets submitted to the system in the following sections:

* _Desk > Branches_. Tickets in the DiamanteDesk are grouped into the **Branches**. Creating separate branches enables our Clients to group tickets according to the requests of specific users, locations, issues or according to the [Channel](../user-guide/channels/index.html) the ticket came from. Open the required branch to see all the tickets that belong to it.

![Tickets in Oro](img/desk_branches.png)

* _Desk > All Tickets_. Tickets can be accessed directly at the **Tickets** section. They are not grouped according to any category on this screen an can be filtered according to the ticket **Key**, **Subject**, **Branch**, **Assignee**, **Priority**, **Status**, or time period when it was **Created** or **Updated**.

![Tickets in Oro](img/all_tickets.png)

* _Customers > Accounts_. Account records referred to as **Accounts** in OroCRM are created to collect and analyze the information on customer activity of a person or group of people belonging to a certain company or organization. Administrators can view all the tickets created or updated by the users belonging to this account at the read-only **Support Tickets** grid in the **Additional Information** section. It displays general ticket information, such as ticket **Key**, **Subject**, **Status**, **Reporter** and date and time when it was updated.

* _Customers > Contacts_. The **Customers** screen contains information about all the customers who created tickets at the [DiamanteDesk portal](../user-guide/channels/portal.html). Administrators can view all the tickets created or updated by the certain customer at the read-only **Support Tickets** grid in the **Additional Information** section. It displays general ticket information, such as ticket **Key**, **Subject**, **Status** and date and time when it was created.

![Tickets in Oro](img/Customers_contacts.png)

<a name="configuration"></a> 
## Configuration

As previously mentioned, when DiamanteDesk is installed on the basis of OroCRM, all the contacts created through the DiamanteDesk support portal are automatically added to the OroCRM contact database. To learn more about contacts in DiamanteDesk, refer to the corresponding section of the [User Guide](../user-guide/customers.html). 

To configure this option, navigate to **System > Configuration**. The **Configuration** screen opens. From the **System Configuration** panel on the left select **DiamanteDesk > Channels**. The **Channels** screen opens. Head over to the **Web** section.

![Web Config](img/web_configuration.png)

To automatically create an Oro contact from the DiamanteDesk contact, select **Yes** option in the **Create Contact Based On Diamante User** and provide a user who is going to be responsible for this action in the **Default Owner** field.