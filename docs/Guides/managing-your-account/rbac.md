---
layout: default
title: RBAC
nav_exclude: true
search_exclude: true
toc_exclude: true
description: Learn about managing RBAC authorization for Firebolt users.
parent: Account and user management
grand_parent: Guides
---

# Role-based access control
{: .no_toc}

Role-based access control provides the ability to control privileges and determine who can access and perform operations on specific objects in Firebolt. Access privileges are assigned to roles that are, in turn, assigned to users. 

A user interacting with Firebolt must have the appropriate privileges to use an object. Privileges from all roles assigned to a user are considered in each interaction with a secured object. 

The key concepts to understanding access control in Firebolt with DB-level RBAC are:

  **Secured object:** an entity to which access can be granted: database, engine subscription.

  **Role:** An entity to which privileges can be granted. Roles are assigned to users.

  **Privilege:** a defined level of access to an object.

  **User:** A user identity recognized by Firebolt. It can be associated with a person or a program. Each user can be assigned multiple roles.

## Role types
Roles are entities to which privileges on securable objects are assigned. Roles are assigned to users to allow them to achieve the required tasks on the relevant objects to fulfill their business needs.

Firebolt comes out of the box with system-defined roles per each account. Those roles cannot be deleted from your account, the same as the privileges granted to the system-defined roles, which cannot be revoked.

Users granted the account admin role can create custom roles to meet specific needs. Moreover, users granted the account admin role can grant roles to other users.

## Privileges
There is a set of privileges that can be granted for every securable object.
### Account

| Privilege         | Description                                    |
|:------------------|:-----------------------------------------------|
| CREATE ENGINE     | Enables creating new engines in the account.   |
| CREATE DATABASE   | Enables creating new databases in the account. |

### Database

| Privilege          | Description |
| :---------------   | :---------- |
| USAGE              | Enables running SELECT on the database's tables, views, and ATTACH engines. |
| MODIFY              | Enables:<br>Running CREATE/DROP tables, views, and indexes on a database's tables.<br>Running INSERT data into a database's tables.<br>Altering the properties of a database.<br>Dropping a database. |

### Engine

| Privilege          | Description |
| :---------------   | :---------- |
| USAGE              | Enables using an engine and, therefore, executing queries on it. |
| OPERATE            | Enables changing the state of an engine (stop, start). |
| MODIFY             | Enables dropping or altering any properties of an engine. |

## System-defined roles

| Role Name      | Description                                                    | Granted Privileges                                                                      |
|:---------------|:---------------------------------------------------------------|:----------------------------------------------------------------------------------------|
| account_admin  | A role that has the privileges to all objects in the account.  | ALL Privileges on Accounts, Users, Roles, Engines and Databases |
| security_admin | Security admin to manage access control                        | ALL Privileges on Accounts, Users, Roles, Engines and Databases                         |
| system_admin   | A role with all database and engine privileges in the account. | Create, Modify and Usage any Engine and Database in the account. can also manage grants |
| public         | default public role                                            | Usage any database                                                                      |

**Custom roles**<br>
A user granted the `account_admin` or `security_admin` roles can create custom roles. 

## Working with roles
### Create a custom role using SQL
`CREATE ROLE <role>`

**Example**
`CREATE ROLE my_role`

Creates a custom role.

| Property           | Description |
| :---------------   | :---------- |
| role               | The name of the role. |

### Create a custom role using the UI
1. In the Firebolt manager, choose the Admin icon in the navigation pane, then choose Role Management.
2. Under Role Name, enter the name of the role.

### Add Database and Engine privileges:
1. Under Role Privileges, choose the secured object you want to manage access for: choose either Databases or Engines respectively.
2. Select the required privileges on the relevant secured object. You can either choose to enable the privilege for a specific object for all existing objects or bulk enable a privilege on all secured objects (this applies to all existing and future objects).

### Delete custom role using SQL
`DROP ROLE <role>`

**Example**
`DROP ROLE my_role`

Deletes a custom role.

| Property           | Description |
| :---------------   | :---------- |
| role               | The name of the role. |


### Delete a custom role using the UI
1. In the Firebolt manager, choose the Admin icon in the navigation pane, then choose Role Management.
2. Locate the custom role you would like to delete, then choose Delete role.

### Managing users' roles
Roles can be granted to users upon creation or after a user is created. Granting roles to new users is done when the user is invited to your account using the UI.

### Manage user’s roles using SQL
`GRANT role to user`
`GRANT ROLE <role> TO USER <user_name>`

**Example**
`GRANT ROLE my_role TO USER “john@acme.com”`

Grants a role to a user.

| Property           | Description |
| :---------------   | :---------- |
| role               | The name of the role. |
| user_name          | The username (email - i.e: john@acme.com) | 


`REVOKE role from user`
`REVOKE ROLE <role> FROM USER <user_name>`

**Example:**
`REVOKE ROLE my_role FROM USER “john@acme.com”`

Revokes a role from a user.

| Property           | Description |
| :---------------   | :---------- |
| role               | The name of the role. |
| user_name          | The username (email - i.e: john@acme.com) | 

### Manage user’s roles using the UI
Managing roles for existing users is performed as follows:
1. In the Firebolt manager, choose the Admin icon in the navigation pane, then choose User Management.
2. Locate the relevant user, then on the right, choose the options icon, then choose Edit user details.
3. Select roles that need to be granted to the user and de-select roles that need to be revoked.
4. Choose Update user details to save the changes.

### Role management
Roles are managed using SQL or on the role management page in Firebolt manager. To get to this page in the Firebolt manager, choose the Admin icon in the navigation pane, then choose Role Management.

### Grant privilege to a role using SQL
`GRANT <privilege> ON { <object_type> <object_name> | ANY <object_type>} TO <role>`
             
**Example**
`GRANT USAGE ON DATABASE my_db TO my_role`

Grant a privilege to a role.

| Property              | Description |
| :---------------      | :---------- |
| privilege             | The privilege. | 
| role                  | The name of the role. |
| object_type           | The type of the secured object (database/engine). | 
| object_name           | The name of the secured object (database/engine). | 
| object_type_in_plural | The type of the secured object in plural(databases/engines). | 

### Grant privilege to a role using the UI
1. Under Role Privileges, choose the secured object you want to manage access for: choose either Databases or Engines respectively.
2. Select the required privileges on the relevant secured object. You can either choose to enable the privilege for a specific object for all existing objects or bulk enable a privilege on all secured objects (this applies to all existing and future objects).

### Revoke privilege from role using SQL
`REVOKE <privilege> ON { <object_type> <object_name> | ANY <object_type>} FROM <role>`

**Example**
`REVOKE USAGE ON DATABASE my_db FROM my_role`

Revokes a privilege from a role.

| Property              | Description |
| :---------------      | :---------- |
| privilege             | The privilege. | 
| role                  | The name of the role. |
| object_type           | The type of the secured object (database/engine). | 
| object_name           | The name of the secured object (database/engine). | 
| object_type_in_plural | The type of the secured object in plural(databases/engines). | 


### Revoke privilege from role using the UI
1. Under Role Privileges, choose the secured object you want to manage access for: choose either Databases or Engines respectively.
2. De-Select the privileges that must be revoked on the relevant secured object. 

## Known limitations and future release plans
 