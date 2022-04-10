# Identity Management

* Comprises
  * Users
  * Roles
    * Sets of permissions
    * Permissions can be assigned **only** to a Role, not User
    * Principle of *Least Privilege*
    * Types of roles:
      * Primitive (basic, not best practice)
        * Owner
        * Editor
        * Viewer
      * Predefined (best practice)
        * Specifically for GCP Products and Services
      * Custom
        * Restrictions on some permissions, e.g. `iam.ServiceAccounts.getAccessToken`
  * Privileges

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
