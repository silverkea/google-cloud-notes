## Learning Resources


### Assigning Users to [[Identity and Access Management (IAM)|IAM]] Roles

You assign members to roles through an IAM policy. Roles are combinations of permissions needed for a role. Members can be a Google account, a service account, a Google group, a Google Workspace domain, a Cloud Identity domain, all authenticated users, and all users. A service account is an account for an application instead of an end user.

IAM lets administrators authorize who can take action on specific resources. An IAM policy has a “who” part, a “can do what” part, and an “on which resource” part.

#### Understanding Roles
The “can do what” part of an IAM policy is defined by a role. An IAM role is a collection of permissions, because, most of the time you need more than 1 permission to do meaningful work. For example, to manage virtual machine instances in a project, you have to be able to create, delete, start, stop and change virtual machines. So these permissions are grouped together into a role to make them easier to understand and easier to manage.

There are three types of roles in IAM:
- Basic roles, which include the Owner, Editor, and Viewer roles that existed prior to the introduction of IAM.
- Predefined roles, which provide granular access for a specific service and are managed by Google Cloud.
- Custom roles, which provide granular access according to a user-specified list of permissions.

Basic roles are the Owner, Editor, and Viewer. If you’re a viewer on a given resource, you can examine it but not change its state. If you’re an editor, you can do everything a viewer can do plus change its state. And if you’re an owner, you can do everything an editor can do plus manage roles and permissions on the resource.

Pre-defined roles bundle selected permissions up into collections that correlate with common job-related business needs.

#### Where to look
https://cloud.google.com/iam/docs/overview 

#### Content mapping
- [Google Cloud Fundamentals: Core Infrastructure (ILT and On-demand)](https://www.cloudskillsboost.google/course_templates/60)
	- M2 Resources and Access in the Cloud
- [Architecting with Google Compute Engine (ILT)](https://cloud.google.com/learn/training/class-schedule#/title=Architecting_with_Google_Compute_Engine)
	- M4 Identity and Access Management
- [Essential Google Cloud Infrastructure: Core Services (On-demand)](https://www.cloudskillsboost.google/course_templates/49)
	- M1 Identity and Access Management
- Skill Badges
	- [Implement Load Balancing on Compute Engine](https://www.cloudskillsboost.google/course_templates/648)
	- [Set Up an App Dev Environment on Google Cloud](https://www.cloudskillsboost.google/course_templates/637)


### Using Organisational Hierarchies

You may find it easiest to understand the Google Cloud resource hierarchy from the bottom up. All the resources you use--whether they’re virtual machines, Cloud Storage buckets, tables in BigQuery, or anything else in Google Cloud--are organized into projects. Optionally, these projects may be organized into folders; folders can contain other folders. 

All the folders and projects used by your organization can be brought together under an organization node. Projects, folders, and organization nodes are all places where policies can be defined. Some Google Cloud resources let you put policies on individual resources too, like Cloud Storage buckets. Policies are inherited downwards in the hierarchy.

When you give a user, group, or service account a role on a specific element of the resource hierarchy, the resulting policy applies to the element you chose, as well as to elements below it in the hierarchy.

#### Organization Policy
Identity and Access Management focuses on who, and lets the administrator authorize who can take action on specific resources based on permissions. 

Organization Policy focuses on what, and lets the administrator set restrictions on specific resources to determine how they can be configured.

A constraint is a particular type of restriction against a Google Cloud service or a list of Google Cloud services. A constraint has a type, either list or Boolean.

When an organization policy is set on a resource hierarchy node, all descendants of that node inherit the organization policy by default. If you set an organization policy at the root organization node, then the configuration of restrictions defined by that policy will be passed down through all descendant folders, projects, and service resources. 

When a child node inherits organization policies based on list constraints, the inherited policies are merged and reconciled with the node's organization policy. In list policy evaluation, DENY values always take precedence. 

Organization policies that are derived from Boolean constraints do not merge and reconcile policies. If a policy is specified on a resource node, that TRUE or FALSE value is used to determine the effective policy.

#### Projects
A project is required to use Google Cloud, and forms the basis for creating, enabling, and using all Google Cloud services, managing APIs, enabling billing, adding and removing collaborators, and managing permissions. 

In order to interact with most Google Cloud resources, you must provide the identifying project information for every request. You can identify a project in either of two ways: a project ID, or a project number. 

A project ID is the customized name you chose when you created the project. If you activate an API that requires a project, you will be directed to create a project or select a project using its project ID. (Note that the name string, which is displayed in the UI, is not the same as the project ID.) 

A project number is automatically generated by Google Cloud. Both the project ID and project number can be found on the dashboard of the project in the Google Cloud console. For information on getting project identifiers and other management tasks for projects see Creating and Managing Projects. 

The initial IAM policy for the newly created project resource grants the owner role to the creator of the project.

#### Where to look
https://cloud.google.com/resource-manager/docs/cloud-platform-resource-hierarchy#resource-hierarchy-detail

https://cloud.google.com/resource-manager/docs/creating-managing-projects

#### Content mapping
- Google Cloud Fundamentals: Core Infrastructure (ILT and On-demand)
	- M2 Resources and Access in the Cloud
- Skill Badge
	- [Implement Load Balancing on Compute Engine](https://www.cloudskillsboost.google/course_templates/648)


### Managing Billing Configuration

Cloud Billing accounts pay for usage costs in Google Cloud projects and Google Maps Platform projects. Cloud Billing accounts do not pay for Google Workspace accounts. 

Google Workspace customers need a separate Google Workspace billing account. A project and its service-level resources are linked to one Cloud Billing account at a time. 

A Cloud Billing account operates in a single currency and is linked to a Google payments profile. 

A Cloud Billing account can be linked to one or more projects.

Usage costs are tracked by Project and are charged to the linked Cloud Billing account. 

Important: Projects that are not linked to an active Cloud Billing account cannot use Google Cloud or Google Maps Platform services. This is true even if you only use services that are free. 

If you want to change the Cloud Billing account that you are using to pay for a project (that is, link a project to a different Cloud Billing account), see Enable, disable, or change billing for a project.

You can manage your Cloud Billing accounts using the Google Cloud console. For more information about the console, visit [General guide to the console](https://support.google.com/cloud/answer/3465889?hl=en&ref_topic=3340599).

#### Budgets

To create a new budget, complete the following steps: 
1. Create and name the budget 
2. Set the budget scope 
3. Set the budget amount 
4. Set the budget threshold rules and actions 
5. Click finish to save the new budget 
 
Threshold rules define the triggering events used to generate a budget notification email. Note that threshold rules are required for email notifications and are used specifically to trigger email notifications. Thresholds rules are not required for programmatic notifications, unless you want your programmatic notifications to include data about the thresholds you set. 

Email notification settings can be either role-based, which sends alerts to the Billing account Administrator and Billing Account Users. This is the default behavior. 

Or you can set up Cloud Monitoring notification channels to send alerts to email addresses of your choice.

#### Where to look

https://cloud.google.com/billing/docs/how-to/manage-billing-account
https://cloud.google.com/billing/docs/how-to/budgets
https://support.google.com/cloud/answer/3465889?hl=en&ref_topic=3340599

#### Content Mapping

- [Google Cloud Fundamentals: Core Infrastructure (ILT and On-demand)](https://www.cloudskillsboost.google/course_templates/60)
	- M2 Resources and Access in the Cloud
- [Architecting with Google Compute Engine (ILT)](https://cloud.google.com/learn/training/class-schedule#/title=Architecting_with_Google_Compute_Engine)
	- M6 Resource Management
- [Essential Google Cloud Infrastructure: Core Services (On-demand)](https://www.cloudskillsboost.google/course_templates/49)
	- M3 Resource Management
