
Administrators can apply policies to define who (Principals) can do what (Roles).

## Principals / Members

Each principal has identifier, usually email address.

- Google account - represents any user who interacts with Google Cloud. Users can sign up without receiving email through Gmail.
- Google group - named collection of google accounts and service accounts. Convenient way to apply policies to a collection of users.
- Services account - account that belongs to application instead of individual user.
- Google Workspace domain - virtual group of all Google accounts created in an organization's Workspace account. 
- Cloud Identity domain - virtual group of all Google accounts created in an organization's Cloud Identity account. Cloud Identity provides ability to manage users in Google Admin console without paying for or receiving Workspace collaboration products like Gmail, Docs, Drive, Calendar.

IAM is not used to create users or groups. This is done in Workspace or Cloud Identity.

### Google Cloud Directory Sync
- Synchronizes users and groups one way from existing AD or LDAP to Cloud Identity domain using same usernames and passwords.
- Designed to be run scheduled once synchronization rules configured.

### Single Sign-On
- Allows using existing identity system to authenticate users. When authentication is required, Google will redirect to the identity provider for authentication.
- Configured in 3 clicks if system supports SAML2, SSO.
- Can also use third party solutions like ADFS, Ping or Okta.

### Service Accounts
- Special type of Google account that belongs to application instead of individual user for service-to service interactions without supplying credentials.
- Applications can automatically acquire access tokens with these credentials
- Tokens are used to access service APIs in project and other services that grant access to service account
- Convenient when not acting on behalf of user.
- Identified by email address.

#### Service Account Types

- User created (custom)
- Built in
	- Compute Engine and App Engine default service account associated with project
	- `{project-number}-compute@developer.gservicesaccount.com`
	- Automatically granted editor permission on project
- Google APIs service account
	- Runs internal Google processes on your behalf
	- Automatically granted the editor role on project
	- `{project-number}@cloudservices.gserviceaccount.com`

##### Scopes
- Used to determine whether an identity is authorized to access a resource.
- Contained by access token.
- Can be customized when creating instance with default service account, or when instance is stopped
- Legacy method of providing permissions for VMs to access Google APIs.
- For user-created service accounts, use IAM roles instead to specify permissions.

##### Service Account Role Assignment to Users / Groups
- Service accounts can be assigned IAM roles to allow users or groups to impersonate them.
- This allows users to perform actions available to the service account.
- Should be used with caution.

##### Service Account Keys
By default Google manages keys for service accounts. If there is need to use service accounts outside Google Cloud, or different rotation period is required, it is also possible to manually create and manage your own service account keys.

Listing service account keys:
```
gcloud iam service-accounts keys list --iam-account user@email.com
```

###### Google Managed Services Account Keys
- Google managed keys
- Public and private key stored by Google
- Public key can be used for signing for two weeks
- Private keys never directly accessible

###### User Managed Service Account Keys
- Google stores public key only
- User responsible for private key security
- Up to 10 user managed keys per service
- Administered via IAM API, `gcloud` or cloud console
- Google cannot assist with recovering private keys
- Should be used as last resort
- Consider alternatives such as short-lived tokens or service account impersonation


## Roles

IAM roles are a collection of permissions. Permissions are the ability to perform specific actions on Google Cloud resources.

When Principal given Role on specific element of resource hierarchy, resulting policy applies to element chosen and elements below in hierarchy.

Roles are collection of permissions, because to do any meaningful operations usually need more than one permission. Grouping in roles makes permissions easier to manage.

Permissions usually align with classes and methods on the APIs. 

### Basic Roles
- Original roles that are available in Cloud console but are broad. 

#### Viewer
- Permissions for read-only actions that do not affect state, such as viewing (but not modifying) existing resources or data.

#### Editor
- All viewer permissions, plus permissions for actions that modify and delete resources, such as changing existing resources.
- e.g. Deploy applications, modify code, configure services, etc

#### Owner
- All editor permissions and permissions for the following actions: manage roles and permissions for a project and all resources within the project; set up billing for a project.
- Includes ability to ad and remove members and delete projects.
- e.g. Invite members, remove members, delete projects, etc

#### Billing Administrator
- Permissions to manage billing for a project, but not permissions to manage Google Cloud resources.
- Can add or remove administrators.

### Predefined Roles

- GCP services offer own set of predefined roles and define where roles can be applied.
- Granular access for specific services. Managed by Google Cloud.
- Can also define where those roles can be applied.
	- e.g. `instanceAdmin` role can be applied to a project, folder or organization for Compute Engine.

#### Example: Compute Engine IAM roles
- Compute Admin: full control of all Compute Engine resources
- Network Admin: create, modify and delete network resources except firewall rules and SSL certificates. Has view access to firewall rules, SSL certificates and instances.
- Storage Admin: create, modify and delete disks, images and snapshots

### Custom Roles
- Support for least privilege model.
- Create roles that meet specific needs.
- Can be defined only at project or organization level, NOT folder level. Organization level custom roles can be applied / assigned at any level of the hierarchy.
- Custom roles have launch stage option to indicate whether the role is in alpha, beta or general availability or disabled.
- Can create role from scratch or start with existing role as base and remove permissions that are not required.
- Custom roles are not automatically updated when new permissions are added to the base role.


## Policies

- Collection of access statements attached to a resource.
- Each policy contains a set of roles and role members, with resources inheriting policies from their parent.
- Act like a union of resource and parent, where less restrictive parent policy will override a more restrictive resource policy.
- Policy hierarchy follows resource hierarchy. Changing the resource hierarchy changes the policy hierarchy.

### Allow Policies
- Used to grant access to resources and any descendants in the resource hierarchy.
- Binds one or more principals with single IAM role and any context-specific conditions that change how and when the role is granted.

### Deny Policies
- Consist of deny rules.
- Deny rules contain a set of principals that are denied permissions, and the permissions they are denied and optional conditions for the permission to be denied.
- When a deny rule is in effect, a principal can't perform the action on the resource, even if they have been granted the permission through an allow policy.

### Conditions
- Define conditional attribute based control for Google Cloud resources.
- Policy only applied if the condition expression evaluates to true.

### Organization Policies
- Configuration of restrictions applied to the organization node and all of its folders and projects.
- Exceptions can be made, but only by user with organization policy administrator role.


## Least Privilege Principle
- Best practice is to follow least privilege principle, where users are given only the permissions they need to perform their job.
- Can use recommender for role recommendations to identify and remove excess permissions from principals. Recommender uses policy insights.


## Organization Restrictions
- Prevent data exfiltration through phishing or insider attacks.
- Restricts access to only resources in authorized Google Cloud organization on managed devices
- Google Cloud admins and egress proxy admins collaborate to set up organization restrictions.
- Managed devices are governed by organization policies of company
- Staff use managed device to access organization resources
- Egress proxy adds organization restriction headers to requests originating from managed devices
- Prevents users from accessing Google Cloud resources in non-authorized organizations
- Organization Restriction feature inspects headers and allows / denies based on organization being accessed
- Can allow access to multiple organizations, e.g. vendor organization


## Best Practices

### Leverage the Resource Hierarchy
- Use project groups that share same trust boundary
- Check policies granted on each resource and understand inheritance
- Use least privilege principle when granting rolls
- Audit policies in Cloud Audit Logs: setiampolicy
- Audit membership of groups used in policies

### Grant Roles to Groups instead of Principals
- Allows updating group membership instead of changing IAM policy
- Audit membership of groups used in policies
- Control ownership of Google group used in IAM policies

### Service Accounts
- Be careful granting `serviceAccountUser` role
- Use names that indicate purpose of service account
- Establish naming convention for service accounts
- Establish key rotation policies
- Audit with `serviceAccount.keys.list()` method

### Identity-Aware Proxy (IAP) - [[Cloud IAP]]
- Central authorization layer for applications accessed by HTTPS
- Provides application level access control model instead of relying on network firewalls
- Enforce access control policies for applications and resources
- Identity-based access control
- Central authorization layer for applications accessed by HTTPS
- IAM policy is applied after authentication











