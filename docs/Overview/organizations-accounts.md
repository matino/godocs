---
layout: default
title: Firebolt organizations and accounts
description: Learn about Firebolt organization and account concepts to help you administer and manage your Firebolt account.
nav_order: 2
parent: Overview
---

# Firebolt organizations and accounts
{: .no_toc}

With organizations, achieve a seamless separation between different accounts within your organization, while benefiting from consolidated billing, unified authentication, and efficient account management across all accounts. 

Learn more about registering with Firebolt and creating your organization [here].

* Topic ToC
{: toc}

## What is an organization?
An organization is a fundamental object in Firebolt, providing a logical structure for managing accounts, billing, and authentication. When registering to Firebolt, the organization name you’ll provide is the same as the domain name you use in your email. Organization names are globally unique—no two organizations can have the same name - but can contain multiple accounts. Each account, in turn, contains users, roles, databases, tables, views, engines, and more.

Firebolt object model image here

Organizations are used to create a structure that fits your needs: by setting up accounts within organizations, you establish a structured framework that aligns with your business needs, data management requirements, and geographical considerations. This allows for better resource allocation, access control, and overall management of your accounts, using:
 
- **Account Hierarchy:** Each organization can contain multiple accounts, allowing you to efficiently organize your data and resources. Each account is identified by its name. 
- **Authentication:** Handle end-user authentication and access control at the organization level. For each end-user a login is created, identified with a login name (represented by an email). 
- **Programmatic access:** Grant programmatic access via [service accounts](../Guides/managing-your-account/service-accounts.md), which can be linked to various accounts by linking a user within an account. 

## What is an account?
An account in Firebolt is an object within an organization that encapsulates resources for storing, querying, and managing data. Accounts provide:
 
- **Region-specific management:** Each account is associated with a specific region, allowing you to store data close to your users and comply with data residency requirements.
- **Data storage resources:** Each account has dedicated resources for securely storing data.
- **Query processing administration:** Engines provide the power to execute queries and process data within each account. Engines are managed at the account level by users with appropriate privileges and can be used according to the account's security policy.
- **Database management:** Users can create databases within an account to organize and structure their data.

## Authentication and access control
Organizations help enforce advanced authentication security policies and ensure compliance across all accounts using network policies, MFA, and SSO to make authentication secure and easy. Users can authenticate using logins for accessing the user interface and service accounts for programmatic access. 

Access control within an account is managed through roles. Roles determine users' access level within an account. By assigning roles to users, admins can control their permissions to perform actions on databases, tables, views, and other objects within the account. This set up allow data governance: regularly reviewing and updating [role-base access control (RBAC)] at the account level helps you remain in conformance with industry regulations and internal standards, and ensures that data are handled, stored, and accessed in a manner that meets compliance requirements.

### Single Sign-On (SSO)
Firebolt offers [Single Sign-On (SSO) functionality], allowing users to log in to the organization using their existing enterprise credentials. This authentication option provides: 
- **Seamless Login Experience:** With SSO, users can log in to Firebolt using their enterprise credentials, eliminating the need to remember and manage separate login credentials.
- **Centralized User Management:** SSO allows you to manage user access and authentication centrally, simplifying user onboarding and offboarding processes. 
- **Enhanced Security:** SSO helps enforce strong authentication standards, and reduces the risk of unauthorized access by leveraging enterprise-grade authentication mechanisms. 

### Network Policies and Multi-Factor Authentication (MFA)
Firebolt enforces network policies and provides multi-factor authentication (MFA) at the organization level to enhance security. This allows: 

- **Network Policies:** [Network policies] help you define and enforce rules regarding inbound and outbound network traffic. This allows you to restrict access to your Firebolt objects based on IP ranges (subnets) or other network-specific parameters. Network policies can be configured for the entire organization, per login, or per service account for more granular restrictions on organizational access, to protect against potential security threats.
- **Multi-Factor Authentication (MFA):** Firebolt supports [multi-factor authentication] at the organization level, adding an extra layer of security to the authentication process and reducing the risk of unauthorized access even if passwords are compromised by requiring users to provide a verification code along with their login credentials. 

## Billing
Firebolt provides billing at the organization level, but gives you billing observability at both organization and account levels. This allows: 

- **Organization Level Governance:** At the organization level, you can monitor and analyze the overall billing for all accounts to gain insights into the organization's cost distribution and resource utilization. 
- **Account Level Observability:** You can delve into detailed billing information specific to each account, allowing you to track individual accounts' usage, costs, storage, and compute consumption patterns.