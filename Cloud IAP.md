Cloud IAP is a Google Cloud service that provides central authentication and authorization for your applications and resources.

## Key features:

- Acts as a security layer in front of applications and services
- Enforces access controls at the application level (not just network level)
- Verifies user identity and context before granting access
- Works with applications running on GCP (App Engine, GKE, Compute Engine)

## Benefits:

- **Zero trust security model**: Validates each request regardless of origin
- **VPN alternative**: Secure access to internal apps without a VPN
- **Granular access control**: Configure permissions at the application level
- **Centralized policy management**: Apply consistent access policies
- **Context-aware access**: Consider factors like device status, IP, time of day

Cloud IAP integrates with Google Cloud's [[Identity and Access Management (IAM)|IAM]] system to determine who can access which applications, providing a comprehensive security solution for controlling access to your cloud resources.