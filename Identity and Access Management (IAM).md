
Administrators can apply policies to define who (Principals) can do what (Roles).

## Principal

Each principal has identifier, usually email address.

- Google account
- Google group
- Services account
- Cloud Identity domain

## Roles

IAM roles are a collection of permissions. Permissions are the ability to perform specific actions on Google Cloud resources.

When Principal given Role on specific element of resource hierarchy, resulting policy applies to element chosen and elements below in hierarchy.

### Deny Rules
Prevent Principals from using permissions regardless of roles assigned.

### Basic Roles

#### Viewer
Permissions for read-only actions that do not affect state, such as viewing (but not modifying) existing resources or data.

#### Editor
All viewer permissions, plus permissions for actions that modify state, such as changing existing resources.

#### Owner
All editor permissions and permissions for the following actions: manage roles and permissions for a project and all resources within the project; set up billing for a project.

#### Billing Administrator
Permissions to manage billing for a project, but not permissions to manage Google Cloud resources.


### Predefined Roles

- Granular access for specific services. Managed by Google Cloud.
- Can also define where those roles can be applied.
	- e.g. `instanceAdmin` role can be applied to a project, folder or organization for Compute Engine.

### Custom Roles
- Support for least privilege model.
- Create roles that meet specific needs.
- Can be applied only at project or organization level, NOT folder level.