
## Topics

### Managing Identity and Access Management (IAM)

#### Assigning Access to Members using IAM

##### Google Account
A google account represents anyone who interacts with Google Cloud. When signing up for a Google account you will be asked to provide an email address that is associated with the account. The email does not have to come from the Gmail domain.

##### Service Account
A service account is how applications and resources authenticate and access services in Google Cloud. Since apps cannot sign in interactively with a username and password, service accounts use keys to authenticate.

##### Google Groups
Collections of identity principals that can be referenced by the email address assigned to the group. You can apply access policies to a group. Each member of the group will receive the permissions you specify in the group policy as they authenticate.

##### Google Workspace and Cloud Identity Domains
Give you the ability to manage users based on the way your organization interacts with Google. Each method gives you a virtual group representing all the registered users in your organization and the ability to add, modify, and delete users and groups.

#### Assign Roles in the IAM Interface

These are the steps to assign roles in the IAM interface. 
- Go to the IAM page 
- Select project, folder, or organization 
- Show info panel if it is not available 
- Click permissions 
- Select or add a principal to add a role to 
	- If the principal already exists click on Add another role
	- For a new principal click add and enter the principals email address 
- Select a role to grant 
- Add a condition 
- Click Save

##### Create Custom Roles

The first thing you need to do when creating custom permissions is be familiar with the permissions and roles that are available in your project or organization.

The `gcloud` command you need to run is:

```
gcloud iam list-testable-permissions
```

To make sure there isn’t already another role that will fill your needs, you can also look at the permissions assigned to a specific role by looking at the role metadata. The role metadata includes the role ID and the permissions associated with that role.

Custom roles can be created at the project or organizational level.

You need to have the `Iam.roles.create` permission. You have to be the owner of the group or project, or have an organization administrator role or the IAM Role Administrator role.

You can create roles from individual permissions, or you can select and pick permissions from predefined roles.

To update an existing role, you run `roles.get()`, update the role locally, and then run `roles.patch()`.


#### Where To Look

https://cloud.google.com/iam/docs/overview
https://cloud.google.com/architecture/prep-kubernetes-engine-for-prod#managing_identity_and_access

#### Content Mapping

- [Google Cloud Fundamentals: Core Infrastructure (ILT and On-demand)](https://www.cloudskillsboost.google/course_templates/60)
	- M2 Resources and Access in the Cloud
- [Architecting with Google Compute Engine (ILT)](https://cloud.google.com/learn/training/class-schedule#/title=Architecting_with_Google_Compute_Engine)
	- M4 Identity and Access Management
- [Essential Google Cloud Infrastructure: Core Services (On-demand)](https://www.cloudskillsboost.google/course_templates/49)
	- M1 Identity and Access Management

- Skill Badge
	- [Develop your Google Cloud Network](https://www.cloudskillsboost.google/course_templates/625)


### Managing Service Accounts

#### Create, use and assign service accounts

##### Creating a Service Account

https://cloud.google.com/iam/docs/creating-managing-service-accounts#creating_a_service_account

To create a service account you use the `gcloud iam service-accounts create` command.

##### Using Service Accounts with IAM Policies

To add a policy to a service account run the `glcloud projects add-iam-policy-binding` command. 

The `--member` argument should be a sting starting with `serviceAccount:` and containing you service account id with and email address suffix of `@project_id.iam.gserviceaccount.com`. A`--role` argument contains the role you want to assign to the service account.

##### Assigning Service Accounts to Resources

Resources in Google Cloud can be assigned to a service account that acts as the resource's default identity. This process is known as attaching a service account to a resource. The resource, or apps running on the resource, impersonate the attached service account to access Google Cloud APIs.

https://cloud.google.com/compute/docs/access/create-enable-service-accounts-for-instances#using

Multiple virtual machine instances can use the same service account, but a virtual machine can only have one service account identity. Service account changes will affect all virtual machine instances using the service account. You can allow access via a cloud-platform scope that allows access to most cloud API’s and then grant the service account the relevant IAM roles.

In `gcloud` you identify the service account you want to use by using the `--service-account` argument.

https://developers.google.com/identity/protocols/oauth2/service-account#python

Two types of keys are available for authentication of a service account: user managed keys and Google managed keys. You create and manage user managed keys yourself. Google only stores the public key.

With Google managed keys Google stores both the public and private portion of the keys. Google has APIs you can use to sign requests with the private key.

#### Types of Authentication Keys

##### API Key
If you are accessing public data, the recommendation is to use an API key.

##### OAuth2.0 Client
If you are accessing private data on behalf of an end user, you should you use the API’s OAuth2.0 client.

##### Environment Provided Service Account
If you are accessing private data on behalf of a service account attached to resources inside a Google Cloud environment, you should use an environment provided service account.

##### Service Account Key
If you are accessing private data on behalf of a service account running outside of Google Cloud, you should create and use a service account key.

#### Where To Look

https://cloud.google.com/docs/authentication/production#automatically
https://cloud.google.com/iam/docs/creating-managing-service-accounts#creating_a_service_account
https://cloud.google.com/compute/docs/access/create-enable-service-accounts-for-instances#using
https://developers.google.com/identity/protocols/oauth2/service-account#python
https://cloud.google.com/docs/authentication/


#### Content Mapping

- [Google Cloud Fundamentals: Core Infrastructure (ILT and On-demand)](https://www.cloudskillsboost.google/course_templates/60)
	- M2 Resources and Access in the Cloud
- [Architecting with Google Compute Engine (ILT)](https://cloud.google.com/learn/training/class-schedule#/title=Architecting_with_Google_Compute_Engine)
	- M4 Identity and Access Management
- [Essential Google Cloud Infrastructure: Core Services (On-demand)](https://www.cloudskillsboost.google/course_templates/49)
	- M1 Identity and Access Management


