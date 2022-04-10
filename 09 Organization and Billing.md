# Organization and Billing

## First things to do

* Creating identities
* Assigning roles
* Setting up billing accounts
* Create Stackdriver Workspace

## Resource Hierarchy

It's a way to group resources and manage them as a single unit

Three levels of Resource Hierarchy:

* Organization - refers to a company or organization
* Folder
* Project

### Organization

* It's a root element of the Resource Hierarchy
* Each Organization has one or none Cloud Identity - IDaaS Google's service
* Is managed by Organization Administrator IAM role users, assigned by Super Admins of Cloud Identity:
* Organization Administrator IAM role user Responsibilities
  * Define structure of Resource Hierarchy
  * Define IAM policies over Resource Hierarchy
  * Delegate roles to other users
* All users in Organization are granted Project Creator and Billing Account Creator roles

### Folder

* Building block of the Resources Hierarchy
* Can be nested
* Should contain either a nested folder or a project
* Normally folder is based on kinds of services

### Project

* The main point in the organization
* Needs to:
  * Create Resources
  * Use Services
  * Manage Permissions
  * Manage billing options
* `resourcemanager.projects.create` is the IAM permission, that allows to create a project
* By default `resourcemanager.projects.create` permission is assigned to every user in the domain of the Organization
* Restricted by a quota, depends on:
  * Usage history
  * Typical use
  * Other factors
* Increase quota via form from Google Cloud Console

## Organization Policies

* It is a Google's service
* Limits of actions related to the resources
* IAM specifies **WHO** can do things, Organization Policy Service specifies **WHAT** can be done with the resource

### Constraints on Resources

* Each resource has it's own constraints list
* Example, deny access to serial ports on VM:
    `constraints/compute.disableSerialPortAccess` `TRUE`
* Constaints may be grouped into Policy and attached it to the Organization
* Organization Policies are *inherited*

## Project Management

* Project is the first step to perform any further action with the Resources

## Billing

* Billing Accounts is a main block of billing
* Billing Accounts store payment information for resources used
* Billing Accounts can be link to >=1 projects
* Billing Accounts must be assigned to a Project, unless Project uses *only* free services
* Types
  * Self-service - automatically paid by credit/debit card - SOHO, personal
  * Invoiced - invoices sent to the customers - enterprises/large customers

### Billing Roles

* Billing Account Creator, can create self-service Billing Account
* Billing Account Administrator, manages Billing Account, NOT create
* Billing Account User, links Projects to Billing Account
* Billing Account Viewer, views Billing Account cost and transactions

### Budgets and Alerts

* Can be set over Project/Billing Account
* Alert default percentage:
  * 50%
  * 90%
  * 100%
* Email will go to
  * Billing Account Administrator
  * Billing Account User
* Notification Pub/Sub topic can be sent (SNS)

### Export Billing Data

* BigQuery DB (AWS RedShift)
* Cloud Storage file (AWS S3)

## API

* API is not enabled by default for a Project
* `APIs & Services` -> `Enable API`
