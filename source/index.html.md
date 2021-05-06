---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - python
  
toc_footers:
  - <a href='https://welkinhealth.com'>Visit our Website</a>
  - <a href='https://github.com/slatedocs/slate'>Documentation Powered by Slate</a>

includes:
  - authentication
  - users
  - users_app_accesses
  - users_policies
  - users_territories
  - patients
  - cdt
  - calendar
  - calendar_events
  - calendar_work_hours
  - calendar_schedule
  - chat
  - emails
  - schedule
  - data_audit
  - security_audit
  - webhook_audit
  - documents
  - encounter
  - care_plans
  - tasks
  - errors
  
search: true

code_clipboard: true
---

# Introduction

<aside class="warning">
Welkin is currently in Closed Beta state, and APIs are subject to changes
</aside>


Welcome to Welkin V8 Release.

When reading this API, we take a liberty and assume that you are familiar with the following Welkin concepts, but for the sake of clarity will shortly repeat them here:

1. **Tenant (Organization)** - This is a customer space, dedicated to one customer. Every customer will have its own tenant that will host customer users, apps and instances
2. **Instance (Environment)** - This is a separate database inside a tenant. Typical customer will have 2-3 instances, representing customer development, testing and live environments, as you build out your Welkin care program
3. **API client** - this is an auto-generated pair of key and secrets, that allows you to access variety of API that Welkin exposes
4. **Security Policies and Roles** - set of rules that dictates what API your client can access and what actions are allowed to be performed
5. **Designer** - Codeless editor for configuring Care Program and all the elements of that program, including Permissions and Roles
6. **Admin** - Admin app that allows one to assign permissions and roles to API clients (among other things)
7. **Care** - Care portal that users will be using to deliver care to patients

For better demonstration of the API, we will use the following setup:

1. Organization (Tenant): **gh**
2. Instance (Environment): **sb-demo**

# Creating API Client
Though this is better covered in our User Guide document, we are going to repeat the steps here, to ensure successful setup

1. Create API client in your Organization 
  * Navigate to Admin -> API Clients -> Create Client
  * Copy the Client Name and Secret Key or download it.

2. Navigate to the API Client page you created
  * Configure appropriate access for the client (Instance Access, Roles, Security Policies)

Reminder: Security Policies and Roles are defined in the Designer and assigned in the Admin

For this example we will assume Client Name is **VBOPNRYRWJIP** and Secret Key is **+}B{KGTG6#zG%P;tQm0C**

