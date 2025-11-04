Terraform is an **Infrastructure as Code (IaC)** tool used to provision and manage Google Cloud resources like VMs, networks, and storage by writing code.
    
- **Declarative, Not Imperative:** Instead of running commands one by one, you create a **declarative configuration file** (e.g., `main.tf`) that defines the _desired state_ of your infrastructure. Terraform then figures out the steps to make that state a reality.
    
- **Core Benefits:**
    
    - **Automation:** Infrastructure can be provisioned and removed automatically, which is ideal for CI/CD pipelines.
        
    - **Consistency:** Easily replicate environments (like dev, test, and prod) from the same code.
        
    - **Speed:** Terraform deploys resources **in parallel**, which is much faster than running sequential commands in Cloud Shell.
        
- **The Basic Workflow:**
    
    1. **Write:** Define your resources in a `.tf` file using the HCL (HashiCorp Configuration Language).
        
    2. **`terraform init`**: Initializes the directory and downloads the required Google provider plugins.
        
    3. **`terraform plan`**: Shows you what Terraform _will_ do (create, change, or destroy) without making any actual changes. This is a "dry run" to check your work.
        
    4. **`terraform apply`**: Executes the plan and creates the infrastructure.

## Reference

[Google Provider Terraform Docs](https://registry.terraform.io/providers/hashicorp/google/latest/docs)

