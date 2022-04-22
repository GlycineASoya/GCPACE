# Identity Management

* Comprises
  * Users
  * Roles
    * Sets of permissions
    * Permissions can be assigned **only** to a Role, not User
    * Principle of *Least Privilege*
    * Types of roles:
      * Primitive (basic, not best practice)
        * Owner - read-only operations, permissions to modify an entry, manage roles, manager permission on an entry, set up Billing for a Project
        * Editor - read-only operations, permissions to modify an entry
        * Viewer - read-only operations
      * Predefined (best practice)
        * Specifically for GCP Products and Services
      * Custom
        * Restrictions on some permissions, e.g. `iam.ServiceAccounts.getAccessToken`
  * Privileges

## Managing Identity and Access Management

* To View:
  * Cloud Console
    * Cloud Console -> IAM & Admin section - get access to IAM resources
  * Cloud SDK (Shell)
    * `gcloud projects get-iam-policy PROJECT_NAME` - get list of the roles assigned to a Project
    * `gcloud iam roles describe roles/RESOURCE.ROLE` - verify permisions for the particular role
* To Assign
  * Cloud Console
    * Cloud Console -> IAM & Admin section -> Roles -> select Role - verify permissions for the particular role
  * Cloud SDK (Shell)
    * `gcloud projects add-iam-policy-binding RESOURCE_NAME --member user:USER_EMAIL --role ROLE_ID` - assigning a role to a memeber in a project
* To Define (a Custom role)
  * Cloud Console
    * Cloud Console -> IAM & Admin section -> Roles -> Create Role
    * Options:
      * Name of the Custom Role
      * Description
      * Identifier
      * Launch stage
        * Alpha
        * Beta
        * General Availability
        * Disabled
      * Set of Permissions
        * Not supported - expected for Custom Roles
        * Supported
  * Cloud SDK (Shell)
    * `gcloud iam roles create ROLE_ID --project PROJECT_NAME --title 'TITLE' --description 'DESCRIPTION' --permissions=appengine.applications.update --stage=STAGE` - creating a role with the permission App Engine Application Update

### Predefined roles

[More info](https://cloud.google.com/iam/docs/understanding-roles)

* App Engine Admin, `roles/appengine.appAdmin` - *read*, *write*, *modify* permission to application and configuration settings
* App Engine Service Admin, `roles/appengine.serviceAdmin` - *read-only* access to configuration setting and *write* access to module-level and version-level settings
* App Engine Deployer, `roles/appengine.deployer` - *read-only* access to application configuration, *write* access to create new version. No *modify*, *delete* versions
* App Engine Viewer, `roles/appengine.appViewer` - *read-only* access to application configuration
* App Engine Code Viewer, `roles/appengine.codeViewer` - *read-only* access to all application configuration and deployed code

## Predefined Useful Roles

* Compute Engine
  * Compute Engine Admin - full control over Compute Engine instances
  * Compute Engine Network Admin - create, modify, delete network resource, read-only access to FW rules and SSL certs
  * Compute Engine Security Admin - create, modify, delete FW rules and SSL certs
  * Compute Engine Viewer - get only the list of Compute Engine instances

## Cloud Identity

* It is a Identity-as-a-Service (IDaaS) Google's service
* Using Cloud Identity G Suite accunt can be managed
* G Suite can be used to create an Organization in [GCP Hierarchy](09_Organization_and_Billing.md)
* Single Cloud Identity is associated with at most one organization (1-1)
* It has super admins that assign Organization Administrator IAM role to users who manage the Organization

## Service Account

* Special user to access a VM/Application
* Service Account is an *Identity* when we assign a role to it
* Service Account is a *Resource* when we give users permission to access it
* There are
  * Google managed SA
  * User managed SA
* Up to 100 SA per Project
* SA created automatically once Resource is created
* IAM Roles and Scope are required to be assigned to get control over VM
* IAM Roles and Scope require to have same set of permissions to allow VM make an operation

### Managing Service Account

* Scopes
  * Permissions granted to a VM to perform some operation
  * Is specified using URL start with `https://www.googleapis.com/auth/`
  * `https://www.googleapis.com/auth/bigquery.insertdata` - scope, allows VM to insert data into BigQuery
  * `https://www.googleapis.com/auth/devstorage.read_only` - scope, allows viewing data in Cloud Storage
  * `https://www.googleapis.com/auth/logging.write` - scope, allows to write to Compute Engine logs
  * Assign Scope on shutdown VM from Cloud Console
  * Assign Scope on VM from Cloud SDK (Shell): `gcloud compute instances set-service-account INSTANCE_NAME [--service-account SERVICE_ACCOUNT_EMAIL | --no-service-account] [--no-scope | --scopes SCOPE1,SCOPE2]`
* Assiging Service Accounts to VMs
  * Cloud Console
    * Create Service Account: Cloud Console -> IAM & Admin -> click Create Service Account
    * Options
      * Name
      * Identifier
      * Description
    * Assign Roles
    * Assign Service Account to VM from VM Instance configuration page, Service Account parameter
  * Cloud SDK (Shell)
    * `gcloud compute instances create INSTANCE_NAME --service-account SERVICE_ACCOUNT_EMAIL`
* Granting access to another Project
