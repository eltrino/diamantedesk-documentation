---
title: User Management
---

**User Management** serves to create new users in DiamanteDesk or to review/edit information about the existing ones. Each user has a certain role, access settings and belongs to one of the existing groups, defining his default permissions in the system.

![User Management](img/user_management.png)

To review the list of all users in the system head over to _System > User Management > Users_:

![User Management](img/all_users.png)

## Create a New User

To create a new user profile in the DiamanteDesk system, head over to _System > User Management > Users_ and click the **Create User** button at the right top corner of the screen or go directly to _System > User Management > Create User_.

![Create User](img/user_new_general.png)

After you get to the **Create User** screen, fill out all the required fields in five following sections, that is **General**, **Additional**, **Groups and Roles**, **Access Settings**, **Email synchronization settings**.

* The **Owner** field is automatically filled with **Main** value by default.
* Select the **Status** of an account - it can be either **Active** or **Inactive**.
* Create a **Username** and **Password** that will be used by a newly created user to log in. **Re-Enter** the password in the following filed to make sure you typed it in correctly.
* Enter a user **Name Prefix**, if required (Mr, Ms, etc.)
* **First Name, Middle Name, Last Name**
* Enter a user **Name Suffix**, if any (for example, Jr., Sr., PMP, etc.)
* Select the **Birthday** from the drop-down calendar in the corresponding field.
* Click the **Avatar** to select a profile picture from your local machine.
* Enter the user's **Primary Email** in the corresponding field. This email is going to be used for email notifications and password recovery. Click **Add Another Email** in the **Emails** field to add additional email in case the primary one is not available for any reason.
* **Email Signature**
* **Phone**
* **Tags.** Tagging functionality is identical throughout the system. To learn more about tagging, follow this [link](tagging.html).

Provide the **Title** (position) of a newly created user in the section for **Additional** information.

![Create User](img/user_new_title.png)

Select the **Groups** and **Roles** the newly created user will belong to. More than one group or role may be selected for one user.

![Create User](img/user_new_groups_roles.png)

### Edit User Account

To edit user account in the DiamnateDesk system:

1. Go to the list of all users in the system at _System > User Management > Users_.
2. Select the user account that shall be changed.
3. Perform the required changes.
4. Click **Save and Close** or **Save** at the right top corner of the screen.

## My Account

To review your account information, click _your username > My User_ at the right top corner of the screen. 

![My User](img/my_user.png)

My account screen opens.

![My User](img/my_account.png)

To edit your account information, click **Edit** at the right top corner of the screen, perform the necessary changes and click **Save**.

## User Roles

When a new user is created within DiamanteDesk, he is assigned with a certain _role_ that determines a set of his permissions and access rights, defining actions a user is allowed to perform. Each user may have one or several roles.

![Role](img/several_roles.png)

To look through the list of available user roles head over to _System > User Management > Roles_.

![Role](img/all_roles.png)

### Permissions

Each role defines the list of actions that may be performed to a certain entity.
 
![Role](img/role_actions.png)

Action | Description
------------- | :-------------
View  | Allows viewing the content of the entity records, grid items.
Create | Allows creating new records for defined entities.
Edit | Allows editing entity records, grid items.
Delete | Allows deleting entity records, grid items.
Assign | Allows assigning the entity records to a different owner.


Permissions may be defined by selecting one of the following options for each entity and the actions that may be performed there.

![Role](img/role_permission_entities.png)

Option | Description
------------- | :-------------
None | None of the users with this role are able to perform the action.
User | Allows the owner-user to perform the corresponding action.
Business Unit | Allows all the users within a business unit to perform the action.
Division | Allows all the users within a division of a business unit to perform the action..
System | Allows all the users with the same role to perform the corresponding action.

###Create a New User Role

1. Navigate to _System > User Management > Roles_.
2. Click **Create Role** at the top right corner of the screen. The **Create Role** screen opens. 
3. Provide the role name, preferably defining the group of users, who will be granted certain permissions (for example, Administrators, Users, etc.) in the **General** tab.
![Role](img/role_name.png)

4. Grant certain permissions by selecting the corresponding options for each action in all entities.
5. The **Capabilities** tab consists of all sorts of functions that may be available for the users. Define what functionalities are available for a user with this role. Users with different roles will see system functionality differently and can perform different actions, accordingly.
![Role](img/role_capabilities.png)
6. Choose the existing users that will be granted this role by selecting the check boxes in the corresponding lines.
7. Click **Save** or **Save and Close** to proceed.

## User Groups

A user group is a collection of user accounts having the same core responsibilities (for example, Administrators, Marketing, Sales). Each user may belong to one or several groups.

![Create Group](img/checked_groups.png) 

To look through the list of available User Groups head over to _System > User Management > Groups_.

### Create a New User Group

1. Go to _System > User Management > Groups_.
2. Click **Create Group** at the right top corner of the screen. The **Create Group** screen opens.
![Create Group](img/create_group.png)
3. The **Owner** field is automatically filled with **Main** value by default.
4. Provide the general name of the group in the **Name** field.
5. Choose the members belonging to this group by selecting the check boxes in the corresponding lines.
6. Click **Save** or **Save and Close** to proceed.