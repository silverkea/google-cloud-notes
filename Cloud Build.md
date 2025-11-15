Cloud Build is a fully managed continuous integration and continuous delivery (CI/CD) service that executes builds on Google Cloud.
    
- **Serverless:** You don't need to provision or manage any servers. It scales automatically to meet demand.
    
- **Container-Native:** It executes builds as a series of Docker container steps. This means you can use any tool that can be packaged in a container as part of your build process.
    
- **Flexible:** It supports building software in any language. It can also deploy to multiple environments, including Compute Engine, App Engine, Kubernetes Engine, and Cloud Functions.
    
- **Secure:** Builds run in a secure, isolated environment. It also integrates with Google Cloud's security features, such as IAM and Secret Manager.
    
- **Integrated:** It works seamlessly with other Google Cloud services and popular developer tools like GitHub, Bitbucket, and GitLab.

![[cloud-build-overview.png]]

## Free Tier

Every day, you get **120 minutes (2 hours) of free build time** per billing account.
#### Important Details

- **Daily Reset:** This allowance resets every 24 hours.
    
- **Specific Machine Types:** The free tier applies _only_ to builds run on the default `e2-medium` machine type. If you configure your builds to use larger, more powerful machines (like `n1-highcpu-8` or `e2-highcpu-32`), you will be billed for every minute of usage, starting from the first minute.
    
- **Per Billing Account:** The 120 minutes are shared across all projects linked to a single Cloud Billing account.
    

For many small projects and CI/CD pipelines, this free tier is sufficient to cover daily build needs without incurring costs.