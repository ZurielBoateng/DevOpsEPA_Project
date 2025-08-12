# EPA Project brief
# This document contians alot of documentation and code snippetsfrom other sources. Mainly the demo applicaiton from OpenTelemetry, and documentation from AWS, Terraform, Kubernetes, and other tooling used. Feel free to use the search function in your editor to find what you are looking for.

This project will provide newcomers of DevOps a chance to work on a real time multi microservice architectured E-commerce application.

The project takes a hands on approach, guiding users through every stage of DevOps in a real world business scenario. From setting up CI/CD pipelines and automating infrastructure to monitoring, security, and scaling, to gain practical experience in solving real challenges faced by e-commerce platforms. 


# Open Telemetry demo application overview, architecture, services, and source code can be found at the following links:
https://opentelemetry.io/docs/demo/
https://opentelemetry.io/docs/demo/architecture/
https://opentelemetry.io/docs/demo/services/
https://github.com/open-telemetry/opentelemetry.io/tree/main#


# **AWS Account Creation Guide**
Creating an Amazon AWS account is required for this project,as wewillbe using its cloud services, other cloud providers work, but for this project we will be using AWS for the specific resources it provides. It is also recommended following the tutoral on AWS to recieve $80-$100 in free credits to use for this project.


# **Step bystepAWS Account Creation**
# **Step 1: Visit the AWS Sign-Up Page**
- Go to [AWS Sign-Up](https://aws.amazon.com/)
- Click on **Create an AWS Account**

# **Step 2: Enter Your Email & Account Details**
- Provide a valid email address
- Choose a **Root user** name
- Set a strong password
- Click **Continue**

# **Step 3: Contact Information**
- Choose **Personal** or **Business** account type
- Fill in your **full name, phone number, and address**
- Click **Continue**

# **Step 4: Payment Information**
- Enter a valid credit or debit card ( required for identity verification)
- AWS may place a small temporary charge for verification
- Click **Continue**

# **Step 5: Identity Verification**
- Enter the **OTP** received via SMS or a phone call
- Complete the CAPTCHA verification
- Click **Verify**

# **Step 6: Choose a Support Plan**
- Select **Basic (Free)**
- Click **Continue**

# **Step 7: Access Your AWS Console**
- Once verified, go to the [AWS Console](https://aws.amazon.com/console/)
- Log in using your email and password

---

# **Next Steps After AWS Account Creation**
- Set up **MFA (Multi-Factor Authentication)** for better security
- Learn about **IAM roles and policies** for access control
- Start with free-tier AWS services like **EC2, S3, Lambda**

---

# **AWS IAM User Creation Guide**
# **Step-by-Step IAM User Creation**

# **Step 1: Log in to AWS Console**
- Go to [AWS Management Console](https://aws.amazon.com/console/)
- Sign in with your **Root Account**
- Navigate to **IAM Dashboard**

# **Step 2: Open IAM Users Section**
- Click on **Users** in the left navigation pane
- Click **Add User**

# **Step 3: Enter User Details**
- Provide a **User Name** (e.g., `devops-user`)
- Select **AWS Credential Type**:
  - **Access Key – Programmatic Access** (for CLI, SDKs, API access)
  - **Password – AWS Management Console Access** (for GUI access)
- Click **Next**

# **Step 4: Assign Permissions**
- Choose how to set permissions:
  - **Attach Existing Policies Directly** (e.g., `AdministratorAccess`, `PowerUserAccess`, `ReadOnlyAccess`)
  - **Add to a Group** (recommended for better management)
  - **Copy from Another User**
- Click **Next**

# **Step 5: Add Tags (Optional)**
- Assign metadata like `Department: DevOps`, `Project: E-Commerce`
- Click **Next**

# **Step 6: Review and Create User**
- Review all details carefully
- Click **Create User**

# **Step 7: Download Credentials**
- Download the **Access Key ID & Secret Access Key**
- Save these credentials securely (they won’t be shown again)
- Click **Close**

--- 

# **AWS EC2 Instance Setup Guide**
# **Introduction**
Amazon EC2 (Elastic Compute Cloud) provides resisable compute capacity in the cloud.
This guide will help in launching an EC2 instance.

---

# **Step-by-Step EC2 Instance Setup**
# **Step 1: Log in to AWS Console**
- Go to [AWS Management Console](https://aws.amazon.com/console/)
- Sign in with your AWS account credentials
- Navigate to **EC2 Dashboard**

# **Step 2: Launch a New EC2 Instance**
- Click **Launch Instance**
- Enter an instance name

# **Step 3: Choose an Amazon Machine Image (AMI)**
- Select an OS (Ubuntu Server 22.04 LTS is recommended)
- Click **Select**

# **Step 4: Choose an Instance Type**
- Select a suitable instance type:
  - **m7i-flex.large** 
- Click **Next**

# **Step 5: Configure Instance Details**
- Keep the default **VPC & Subnet** (unless customising networking)
- Enable **Auto-assign Public IP** (for internet access)
- Click **Next**

# **Step 6: Add Storage**
- Default storage: 8GB, change to 30 GB for more storage for container images.
- Click **Next**

# **Step 7: Configure Security Group**
- Create a new security group or use an existing one
- Allow **SSH (port 22)** for Linux instances

# **Step 8: Generate or Select a Key Pair**
- Select **Create a new key pair**
- Choose **RSA** format and download the `.pem` file
- **Store the key securely** (It is need to access the instance)
- Click **Launch Instance**

# **Step 9: Connect to Your EC2 Instance**
- Navigate to **EC2 Dashboard** → **Instances**
- Select the instance and click **Connect**

# **For Linux Instances:**
- Use SSH from terminal:
  ```bash
  ssh -i /path/to/your-key.pem ec2-user@your-instance-public-ip
  ```

---

# Docker Installation on Ubuntu EC2
# Add Docker's official GPG key:
```
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc
```

# Add the repository to Apt sources:
```
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "${UBUNTU_CODENAME:-$VERSION_CODENAME}") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
```

# Install Docker
```
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

# Verify Docker Installation
```
sudo docker run hello-world

```
# Kubectl Installation on Ubuntu EC2
# Download kubectl
```
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
```

# Install Kubectl
```
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
```

# Verify Kubectl
```
kubectl version --client
```

# Install Terraform on Ubuntu EC2
# Add Hashicorp repos
```
sudo apt-get update && sudo apt-get install -y gnupg software-properties-common

wget -O- https://apt.releases.hashicorp.com/gpg | \
gpg --dearmor | \
sudo tee /usr/share/keyrings/hashicorp-archive-keyring.gpg > /dev/null

echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] \
https://apt.releases.hashicorp.com $(lsb_release -cs) main" | \
sudo tee /etc/apt/sources.list.d/hashicorp.list

sudo apt update
```

# Install Terraform
```
sudo apt-get install terraform
```

# Verify Terraform Installation
```
terraform -help
```

# Run the project Locally
# Clone the repository
```git clone https://github.com/open-telemetry/opentelemetry.io.git
cd opentelemetry.io
```
Make sure you are in the directory of cloned repo and run `docker compose up`
Use the `docker compose` command which is installed as part of `docker`.
If you are using Docker Desktop(likley on a Windows machine), you can also use the `docker compose` command directly in your terminal.

This will start the application locally, and it can be accessed at `http://localhost:1313/`.


# Expose project on EC2 instance
# **Step 1: Log in to AWS Console**
- Go to [AWS Management Console](https://aws.amazon.com/console/)
- Navigate to **EC2 Dashboard**
- Click on **Security Groups** under **Network & Security**

# **Step 2: Select the Security Group**
- Identify and select the Security Group associated with your EC2 instance
- Click on the **Inbound rules** tab
- Click **Edit inbound rules**

# **Step 3: Add a New Inbound Rule**
- Click **Add Rule**
- Select **Type** (Choose a predefined rule like HTTP, SSH, or Custom)
- Select **Protocol** (Automatically populated based on Type)
- Enter **Port Range** (e.g., `80` for HTTP, `22` for SSH, `8080` for custom apps)
- Select **Source**:
  - `My IP` (restrict access to your IP)
  - `Custom` (specify a range like `192.168.1.0/24`)
  - `Anywhere (0.0.0.0/0)` (allows access from any IP, not recommended for production)
- Click **Save rules**

# **Step 4: Verify the Changes**
- Ensure the rule appears in the **Inbound Rules** list
- Test connectivity by accessing the instance on the exposed port


# Docker Lifecycle
Docker follows a structured lifecycle that enables efficient application deployment. 
The three fundamental steps in the Docker lifecycle are:

# 1. Dockerfile Creation  
A **Dockerfile** is a text based script containing a set of instructions that define how a Docker image should be built. It specifies the base image, dependencies, environment configurations, and the command to run the application. The Dockerfile ensures consistency by automating the image creation process.

# 2. Docker Image Build  
Using the **Dockerfile**, a **Docker image** is created through the `docker build` command. A Docker image is a lightweight, standalone, and executable package that includes everything needed to run an application, such as the runtime environment, system tools, libraries, and dependencies.

# 3. Run the Docker Container  
Once the image is built, a **Docker container** is created and executed using the `docker run` command. A container is an isolated environment where the application runs consistently across different systems. Containers leverage the lightweight nature of Docker images, ensuring minimal overhead and fast deployment.


# Containeristion of a different programming language based microservices
For the project we will go over 3 different microservices, each written in a different programming language. We will go over Go, Java, and Python. This will give you a chance to see how containerization works with different languages and frameworks. Feel free to explore and try containerising the other microservices in the project that use different languages.

# Containerization of a Golang based microservice
- The **first stage** compiles the Go microservice efficiently with caching mechanisms.  
- The **second stage** runs the built application in a **lightweight, production-ready environment**.  
- Using **multi-stage builds** ensures that the final image contains only what is needed, making it **small, secure, and optimized** for production.  

# **Stage 1: Build Stage (Builder Image)**  
This stage is responsible for **compiling the Go application** in an optimized manner.  

1. **Use a Minimal Go Base Image**  
   - The `golang:1.22-alpine` image is used for building the application.  
   - Alpine is a lightweight Linux distribution that helps reduce image size.  

2. **Set the Working Directory**  
   - The working directory inside the container is set to `/usr/src/app/`.  

3. **Enable Go Build Cache**  
   - `--mount=type=cache,target=/go/pkg/mod` caches Go modules to speed up dependency management.  
   - `--mount=type=cache,target=/root/.cache/go-build` caches compiled build artifacts for efficiency.  
   - This helps avoid unnecessary re-downloading and recompiling.  

4. **Copy Go Module Files**  
   - The `go.mod` and `go.sum` files are copied to ensure dependencies are managed correctly.  

5. **Download Dependencies**  
   - `go mod download` fetches all required dependencies before copying the entire source code.  

6. **Copy the Rest of the Source Code**  
   - The entire Go project is copied into the container.  

7. **Build the Go Application**  
   - `go build -o product-catalog .` compiles the Go application and outputs an executable binary.  

---

# **Stage 2: Runtime Stage (Final Image)**  
This stage creates a **minimal runtime environment** for running the compiled Go binary.  

1. **Use a Minimal Alpine Base Image**  
   - The `alpine` image is used to keep the final image size as small as possible.  

2. **Set the Working Directory**  
   - The working directory remains `/usr/src/app/`.  

3. **Copy Required Files from the Build Stage**  
   - The `./products/` directory is copied (likely containing static data or configurations).  
   - The compiled `product-catalog` binary from the `builder` stage is copied to the final image.  

4. **Set Environment Variables**  
   - `PRODUCT_CATALOG_PORT` is set to `8088`, defining the port the service will listen on.  

5. **Define the Entry Point**  
   - The container executes `./product-catalog`, starting the Go microservice.  

---

# Containerization of a Java based microservice
- The **first stage** builds the application using Gradle.  
- The **second stage** runs the built application inside a **lightweight JRE-based image**.  
- Using **multi-stage builds** ensures that the final image only contains what is necessary for execution, making it **smaller, more secure, and optimized** for production use.  

# **Explanation of the Multi-Stage Dockerfile for a Java Microservice (Using Gradle)**  
# **Stage 1: Build Stage (Builder Image)**  
This stage is responsible for **building the Java application** using Gradle.  

1. **Use a JDK Base Image**  
   - The `eclipse-temurin:21-jdk` image is used as the build environment.  
   - This includes the necessary Java Development Kit (JDK) to compile the application.  

2. **Set the Working Directory**  
   - The working directory inside the container is set to `/usr/src/app/`.  

3. **Copy Essential Gradle Files**  
   - The `gradlew`, `settings.gradle`, and `build.gradle` files are copied to the container.  
   - The `gradle` wrapper directory is also copied to ensure Gradle can be executed inside the container.  

4. **Set Execution Permissions for Gradlew**  
   - The `chmod +x ./gradlew` command ensures the Gradle wrapper script has execution permissions.  

5. **Initialize Gradle and Download Dependencies**  
   - `./gradlew` runs the Gradle wrapper, setting up necessary configurations.  
   - `./gradlew downloadRepos` ensures that required repositories are downloaded to speed up the build.  

6. **Copy the Application Source Code**  
   - The entire project source code is copied to the container.  
   - The `pb` directory is copied into the container as `proto` (likely for protocol buffer files).  

7. **Build the Application**  
   - `./gradlew installDist -PprotoSourceDir=./proto` compiles and packages the Java application.  
   - The `-PprotoSourceDir=./proto` flag specifies the location of protocol buffer files.  

---

# **Stage 2: Runtime Stage (Final Image)**  
This stage creates a **lightweight, optimized runtime image** for running the application.  

1. **Use a Minimal JRE Base Image**  
   - The `eclipse-temurin:21-jre` image is used since it contains only the Java Runtime Environment (JRE), reducing the final image size.  

2. **Set the Working Directory**  
   - The working directory remains `/usr/src/app/`.  

3. **Copy the Built Application from the Builder Stage**  
   - The compiled application from the `builder` stage is copied into the final image.  

4. **Set Environment Variables**  
   - The `AD_PORT` environment variable is set to `9099`.  

5. **Define the Entry Point**  
   - The application is executed with `./build/install/opentelemetry-demo-ad/bin/Ad`.  
   - This is the compiled and installed binary from the Gradle `installDist` task.  

---

# Containerization of a Python based microservice
- The **Dockerfile** sets up a **lightweight Python environment** with all necessary dependencies.  
- The **OpenTelemetry auto-instrumentation** is installed for monitoring.  
- The final image runs the **Python microservice efficiently** with minimal overhead.

# **Stage 1: Base Image Setup**  
This stage is responsible for **setting up the environment and installing dependencies** for the Python application.  

1. **Use a Minimal Python Base Image**  
   - The `python:3.12-slim-bookworm` image is used to keep the container lightweight.  
   - "Slim" versions of Python images contain only essential packages, reducing image size.  

2. **Set the Working Directory**  
   - The working directory inside the container is set to `/usr/src/app/`.  

3. **Copy Dependency File**  
   - The `requirements.txt` file is copied into the container to install dependencies.  

4. **Upgrade Pip**  
   - `pip install --upgrade pip` ensures that the latest version of `pip` is used.  

5. **Install Dependencies**  
   - `pip install -r requirements.txt` installs all required Python packages.  

6. **Copy the Application Source Code**  
   - The entire project source code is copied into the container.  

7. **Install OpenTelemetry Dependencies**  
   - `opentelemetry-bootstrap -a install` installs OpenTelemetry auto-instrumentation for tracing and monitoring.  

8. **Set Environment Variables**  
   - `RECOMMENDATION_PORT` is set to `1010`, defining the port the service will use.  

9. **Define the Entry Point**  
   - The application is executed with `python recommendation_server.py`.  
   - This runs the Python microservice when the container starts.  

---

# Kubernetes
Kubernetes is a powerful container orchestration platform that automates the deployment, scaling, and management of containerized applications. It provides a robust framework for running applications in a distributed environment, ensuring high availability and efficient resource utilization.

- **Docker runs containers**, but they are temporary and need manual management.  
- **Kubernetes automates** scaling, healing, and service discovery.  
- With Kubernetes, applications are **more reliable, scalable, and selfhealing**.

# Container Orchestration
- **Kubernetes** is designed for **complex, multi hostenvironments** and large scale applications.
- It automates the deployment, scaling, and management of containers across a **cluster of machines**.  


# Terraform code 
Complete terraform files to create EKS in AWS VPC is available in the `eks-install` folder of the repoThis includes remote backend and statelocking implementation as well.

- `eks-install`: Folder that holds the complete terraform hcl files.
- `backend`: Folder that holds hcl files for s3 bucket and dynamodb creation.
- `modules`: Terraform Modules for VPC and EKS.
- `main.tf`: Main file that invokes the modules to create EKS in VPC.
- `variables.tf`: Variables for main.tf
- `outputs.tf`: Output values you wish to see post terraform execution, For example - `VPC ID`.

# Useful plugins to write HCL files
- `Terraform`
- `YAML`
- `GitHub Copilot`

# Documentation
- For any additional help, Terraform official documentation for AWS Provider is the best place.

# Terraform Lifecycle
Terraform follows a well deninedlifecycle for managing infrastructure as code. The lifecycle consists of several stages that ensure resources are created, updated, or destroyed in a controlled manner.

# 1. **Initialization (`terraform init`)**
- Prepares the working directory for Terraform operations.
- Downloads required provider plugins and modules.
- Configures the backend for storing state files.

# 2. **Planning (`terraform plan`)**
- Analyzes the existing state and the desired configuration.
- Shows a preview of what actions Terraform will take.
- Helps in reviewing changes before applying them.

# 3. **Application (`terraform apply`)**
- Executes the planned changes to create, update, or destroy resources.
- Stores the updated state in the backend.

# Connect Terraform with AWS to Create AWS Resources
# 1. **Install AWS CLI**
# On Linux:
- Download and install AWS CLI:
  ```sh
  curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
  unzip awscliv2.zip
  sudo ./aws/install
  ```
- Verify installation:
  ```sh
  aws --version
  ```

# On Windows:
- Download the installer from [AWS CLI Official Site](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html)
- Run the installer and follow the setup instructions.
- Verify installation:
  ```sh
  aws --version
  ```

# 2. **Configure AWS CLI**
- Run the following command to configure AWS credentials:
  ```sh
  aws configure
  ```
- Provide the following details when prompted:
  - AWS Access Key ID
  - AWS Secret Access Key
  - Default region name (e.g., `us-east-1`)
  - Default output format (e.g., `json` or `text`)

**NOTE**: Above command stores AWS credentials in `~/.aws/credentials`, Terraform uses those credentails to interact with AWS.

# Terraform Statefile: The Brain of Terraform
# **What is a Terraform Statefile?**
- Terraform maintains a statefile (`terraform.tfstate`) that records information about managed infrastructure.
- It acts as the single source of truth for Terraform and helps track resource mappings between Terraform configurations and real-world infrastructure.
**Tracking Resources:** Terraform uses the statefile to understand which resources it manages.
- **Performance Optimization:** Instead of querying cloud providers every time, Terraform reads from the statefile to improve performance.
- **Dependency Management:** It helps Terraform determine resource dependencies and execution order.


# Managing Terraform Statefile using S3 Bucket and DynamoDB
Terraform stores its statefile locally by default, which can lead to several issues:
1. **Collaboration Challenges**: When multiple users work on the same Terraform project, local statefiles create inconsistencies.
2. **Risk of Data Loss**: If the local statefile is deleted or corrupted, the infrastructure mapping is lost.
3. **Concurrency Issues**: Multiple users running Terraform commands simultaneously can cause conflicts and unintended changes.
4. **Security Concerns**: Local statefiles may contain sensitive information, making them vulnerable to unauthorized access.

To overcome these challenges, Terraform provides remote state management using an **Amazon S3 bucket** for storage and **DynamoDB** for state locking.

# **Managing Terraform Statefile using S3 and DynamoDB**
# **1. Create an S3 Bucket for State Storage**
- Ensure the bucket is in a region close to your infrastructure for better performance.
- Enable versioning to retain state history and rollback when needed.

# **2. Create a DynamoDB Table for State Locking**
- Define a table with a primary key (`LockID`).
- Ensure that DynamoDB has provisioned throughput or is configured to use on-demand capacity.

# **3. Configure the Terraform Backend**
- Define the S3 backend in Terraform with the following:
  - `bucket` (S3 bucket name)
  - `key` (statefile path in S3)
  - `region` (AWS region)
  - `dynamodb_table` (DynamoDB table for locking)

# **4. Apply the Terraform Configuration**
- Run `terraform init` to initialize the backend.
- Terraform will store the state in S3 and use DynamoDB to prevent race conditions.

By following this setup, Terraform state management becomes more secure, reliable, and scalable for team collaboration.

# S3 Bucket for Remote backend
# **Problem with Local Statefile**
By default, Terraform stores its statefile (`terraform.tfstate`) locally on the machine where Terraform is executed. This approach has several issues:
1. **Risk of Data Loss**: If the local machine crashes or the file is accidentally deleted, the statefile is lost.
2. **Collaboration Challenges**: When multiple users work on the same Terraform project, local statefiles can lead to inconsistencies and conflicts.
3. **Concurrency Issues**: If two users apply changes simultaneously, the statefile may become corrupted.
4. **Security Risks**: Local statefiles may contain sensitive data (e.g., resource IDs, credentials) that could be exposed.

# **How S3 Bucket Solves These Problems**
1. **Centralized Storage**: The statefile is stored in a remote S3 bucket, making it accessible to all team members.
2. **Versioning Support**: S3 enables versioning, allowing rollback to previous state versions if needed.
3. **State Consistency**: When used with DynamoDB for state locking, S3 prevents simultaneous modifications, avoiding corruption.
4. **Security & Backup**: S3 supports encryption and automated backups, reducing security risks and ensuring recovery options.
5. **Scalability**: S3 can handle large statefiles efficiently without performance issues.

# Dynamodb for state locking
# **Problem with No State Locking**
When multiple users or processes run Terraform at the same time, several issues can arise:
1. **Concurrency Conflicts**: If two users apply changes simultaneously, they might overwrite each other's changes, leading to inconsistencies.
2. **State Corruption**: Without locking, partial updates can occur, resulting in a corrupted statefile.
3. **Unreliable Infrastructure Changes**: Race conditions can cause Terraform to misinterpret infrastructure state, leading to unintended modifications.

# **How DynamoDB Solves These Problems**
1. **State Locking**: DynamoDB creates a lock entry when Terraform applies changes, preventing concurrent modifications.
2. **Ensures Consistency**: Only one process can modify the statefile at a time, ensuring consistency and preventing corruption.
3. **Automatic Lock Release**: When Terraform execution completes, the lock entry is removed, allowing the next process to proceed.
4. **High Availability**: As a managed AWS service, DynamoDB provides reliable and scalable state locking.
5. **Cost Efficiency**: With `PAY_PER_REQUEST` billing, DynamoDB incurs minimal cost for Terraform state locking.

# Code explanation for S3 bucket and DynamoDB terraform file
# **1. AWS Provider Configuration**
```hcl
provider "aws" {
  region = "eu-west-2"
}
```
- This block defines the **AWS provider** that Terraform will use.
- The `region` attribute specifies the AWS region where resources will be created (in this case, `eu-west-2`).

---

# **2. Creating an S3 Bucket for Terraform State Storage**
```hcl
resource "aws_s3_bucket" "terraform_state" {
  bucket = "demo-terraform-eks-state-bucket"

  lifecycle {
    prevent_destroy = false
  }
}
```
- This block creates an **S3 bucket** named `demo-terraform-eks-state-bucket`.
- The `lifecycle` rule with `prevent_destroy = false` allows Terraform to delete the bucket when required.

---

# **3. Enabling Versioning for the S3 Bucket**
```hcl
resource "aws_s3_bucket_versioning" "terraform_state" {
  bucket = aws_s3_bucket.terraform_state.id
  versioning_configuration {
    status = "Enabled"
  }
}
```
- This block enables **versioning** on the S3 bucket to retain previous versions of the Terraform statefile.
- Helps with rollback and recovery in case of accidental changes.

---

# **4. Enabling Server-Side Encryption for the S3 Bucket**
```hcl
resource "aws_s3_bucket_server_side_encryption_configuration" "terraform_state" {
  bucket = aws_s3_bucket.terraform_state.id

  rule {
    apply_server_side_encryption_by_default {
      sse_algorithm = "AES256"
    }
  }
}
```
- This block **enables encryption** using the `AES256` algorithm to protect statefile data at rest.
- Ensures that Terraform statefiles are stored securely in the S3 bucket.

---

# **5. Creating a DynamoDB Table for State Locking**
```hcl
resource "aws_dynamodb_table" "terraform_locks" {
  name         = "terraform-eks-state-locks"
  billing_mode = "PAY_PER_REQUEST"
  hash_key     = "LockID"

  attribute {
    name = "LockID"
    type = "S"
  }
}
```
- This block creates a **DynamoDB table** named `terraform-eks-state-locks`.
- The table is used for **state locking**, preventing concurrent modifications to the statefile.
- `billing_mode = "PAY_PER_REQUEST"` ensures cost-effective pricing based on actual usage.
- The primary key (`hash_key`) is `LockID`, ensuring unique entries for locks.

# Terraform Modular approach benifits

# **What is Terraform Modular Approach?**
Terraform's modular approach allows infrastructure to be broken down into reusable and maintainable components called **modules**. Instead of writing everything in a single configuration file, modules help in structuring code for better scalability and reusability.

# **Advantages of Using Modules in Terraform**

# **1. Reusability**
- Modules can be reused across multiple projects, reducing redundant code.
- Example: A **VPC module** can be used for different environments (dev, staging, production) without rewriting the VPC configuration each time.

# **2. Maintainability**
- Simplifies management by keeping infrastructure code organized.
- Example: An **EKS module** can be separately managed, updated, and versioned without affecting other resources.

# **3. Scalability**
- Easier to scale infrastructure as modules allow independent provisioning.
- Example: Scaling an **EKS cluster** without modifying the entire Terraform configuration.

# **4. Team Collaboration**
- Different teams can work on different modules independently.
- Example: The networking team can manage the **VPC module**, while the DevOps team configures the **EKS module**.

# **5. Consistency and Best Practices**
- Modules enforce standardized infrastructure patterns.
- Example: A **VPC module** ensures that all environments follow the same networking architecture.

# Code explanation for VPC module

# **1. Creating a VPC**
```hcl
resource "aws_vpc" "main" {
  cidr_block           = var.vpc_cidr
  enable_dns_hostnames = true
  enable_dns_support   = true

  tags = {
    Name                                           = "${var.cluster_name}-vpc"
    "kubernetes.io/cluster/${var.cluster_name}"    = "shared"
  }
}
```
- Creates a **VPC (Virtual Private Cloud)** using the CIDR block specified in `var.vpc_cidr`.
- Enables **DNS support** and **DNS hostnames** for instances in the VPC.
- Adds tags for Kubernetes cluster integration and identification.

---

# **2. Creating Private Subnets**
```hcl
resource "aws_subnet" "private" {
  count             = length(var.private_subnet_cidrs)
  vpc_id            = aws_vpc.main.id
  cidr_block        = var.private_subnet_cidrs[count.index]
  availability_zone = var.availability_zones[count.index]

  tags = {
    Name                                           = "${var.cluster_name}-private-${count.index + 1}"
    "kubernetes.io/cluster/${var.cluster_name}"    = "shared"
    "kubernetes.io/role/internal-elb"              = "1"
  }
}
```
- Creates multiple **private subnets** based on `private_subnet_cidrs`.
- Each subnet is assigned an **availability zone** from `availability_zones`.
- Tags define Kubernetes cluster association and **internal load balancer** role.

---

# **3. Creating Public Subnets**
```hcl
resource "aws_subnet" "public" {
  count             = length(var.public_subnet_cidrs)
  vpc_id            = aws_vpc.main.id
  cidr_block        = var.public_subnet_cidrs[count.index]
  availability_zone = var.availability_zones[count.index]

  map_public_ip_on_launch = true

  tags = {
    Name                                           = "${var.cluster_name}-public-${count.index + 1}"
    "kubernetes.io/cluster/${var.cluster_name}"    = "shared"
    "kubernetes.io/role/elb"                       = "1"
  }
}
```
- Creates multiple **public subnets** based on `public_subnet_cidrs`.
- Assigns **public IP addresses** to instances on launch.
- Tags specify Kubernetes cluster association and **public load balancer** role.

---

# **4. Creating an Internet Gateway**
```hcl
resource "aws_internet_gateway" "main" {
  vpc_id = aws_vpc.main.id

  tags = {
    Name = "${var.cluster_name}-igw"
  }
}
```
- Creates an **Internet Gateway** to enable internet access for public subnets.

---

# **5. Creating NAT Gateway and Elastic IPs**
```hcl
resource "aws_eip" "nat" {
  count = length(var.public_subnet_cidrs)
  domain = "vpc"

  tags = {
    Name = "${var.cluster_name}-nat-${count.index + 1}"
  }
}

resource "aws_nat_gateway" "main" {
  count         = length(var.public_subnet_cidrs)
  allocation_id = aws_eip.nat[count.index].id
  subnet_id     = aws_subnet.public[count.index].id

  tags = {
    Name = "${var.cluster_name}-nat-${count.index + 1}"
  }
}
```
- **Elastic IPs (EIPs)** are created for the **NAT gateways**.
- **NAT gateways** allow private subnet instances to access the internet securely.
- Each NAT gateway is associated with a **public subnet**.

---

# **6. Creating Route Tables**
```hcl
resource "aws_route_table" "public" {
  vpc_id = aws_vpc.main.id

  route {
    cidr_block = "0.0.0.0/0"
    gateway_id = aws_internet_gateway.main.id
  }

  tags = {
    Name = "${var.cluster_name}-public"
  }
}
```
- **Public route table** routes internet traffic (`0.0.0.0/0`) to the Internet Gateway.

```hcl
resource "aws_route_table" "private" {
  count  = length(var.private_subnet_cidrs)
  vpc_id = aws_vpc.main.id

  route {
    cidr_block     = "0.0.0.0/0"
    nat_gateway_id = aws_nat_gateway.main[count.index].id
  }

  tags = {
    Name = "${var.cluster_name}-private-${count.index + 1}"
  }
}
```
- **Private route tables** route internet traffic through **NAT gateways**.

---

# **7. Associating Route Tables with Subnets**
```hcl
resource "aws_route_table_association" "private" {
  count          = length(var.private_subnet_cidrs)
  subnet_id      = aws_subnet.private[count.index].id
  route_table_id = aws_route_table.private[count.index].id
}
```
- Associates each **private subnet** with a **private route table**.

```hcl
resource "aws_route_table_association" "public" {
  count          = length(var.public_subnet_cidrs)
  subnet_id      = aws_subnet.public[count.index].id
  route_table_id = aws_route_table.public.id
}
```
- Associates all **public subnets** with the **public route table**.

# Code explanation for EKS module

# **1. Creating IAM Role for EKS Cluster**
```hcl
resource "aws_iam_role" "cluster" {
  name = "${var.cluster_name}-cluster-role"

  assume_role_policy = jsonencode({
    Version = "2012-10-17"
    Statement = [{
      Action = "sts:AssumeRole"
      Effect = "Allow"
      Principal = {
        Service = "eks.amazonaws.com"
      }
    }]
  })
}
```
- Creates an **IAM role** for the EKS cluster.
- Allows **Amazon EKS** to assume this role for managing cluster operations.

---

# **2. Attaching IAM Policy to Cluster Role**
```hcl
resource "aws_iam_role_policy_attachment" "cluster_policy" {
  policy_arn = "arn:aws:iam::aws:policy/AmazonEKSClusterPolicy"
  role       = aws_iam_role.cluster.name
}
```
- Attaches **AmazonEKSClusterPolicy** to the EKS cluster role.
- Grants necessary permissions for EKS to manage the cluster.

---

# **3. Creating the EKS Cluster**
```hcl
resource "aws_eks_cluster" "main" {
  name     = var.cluster_name
  version  = var.cluster_version
  role_arn = aws_iam_role.cluster.arn

  vpc_config {
    subnet_ids = var.subnet_ids
  }

  depends_on = [
    aws_iam_role_policy_attachment.cluster_policy
  ]
}
```
- Creates an **EKS cluster** with the specified name and version.
- Uses the IAM role created earlier for authorization.
- Associates the cluster with **VPC subnets** for networking.
- **Depends on** the IAM policy attachment to ensure permissions are set.

---

# **4. Creating IAM Role for Node Group**
```hcl
resource "aws_iam_role" "node" {
  name = "${var.cluster_name}-node-role"

  assume_role_policy = jsonencode({
    Version = "2012-10-17"
    Statement = [{
      Action = "sts:AssumeRole"
      Effect = "Allow"
      Principal = {
        Service = "ec2.amazonaws.com"
      }
    }]
  })
}
```
- Creates an **IAM role** for the EKS worker nodes.
- Allows **EC2 instances** to assume this role.

---

# **5. Attaching IAM Policies to Node Role**
```hcl
resource "aws_iam_role_policy_attachment" "node_policy" {
  for_each = toset([
    "arn:aws:iam::aws:policy/AmazonEKSWorkerNodePolicy",
    "arn:aws:iam::aws:policy/AmazonEKS_CNI_Policy",
    "arn:aws:iam::aws:policy/AmazonEC2ContainerRegistryReadOnly"
  ])

  policy_arn = each.value
  role       = aws_iam_role.node.name
}
```
- Attaches **three AWS managed policies** to the worker node role:
  1. **AmazonEKSWorkerNodePolicy** - Grants permissions to join and interact with the EKS cluster.
  2. **AmazonEKS_CNI_Policy** - Allows the container network interface to operate properly.
  3. **AmazonEC2ContainerRegistryReadOnly** - Grants access to pull container images from ECR.

---

# **6. Creating EKS Node Group**
```hcl
resource "aws_eks_node_group" "main" {
  for_each = var.node_groups

  cluster_name    = aws_eks_cluster.main.name
  node_group_name = each.key
  node_role_arn   = aws_iam_role.node.arn
  subnet_ids      = var.subnet_ids

  instance_types = each.value.instance_types
  capacity_type  = each.value.capacity_type

  scaling_config {
    desired_size = each.value.scaling_config.desired_size
    max_size     = each.value.scaling_config.max_size
    min_size     = each.value.scaling_config.min_size
  }

  depends_on = [
    aws_iam_role_policy_attachment.node_policy
  ]
}
```
- Creates an **EKS Node Group** to run worker nodes within the cluster.
- Assigns **node IAM role** for permissions.
- Uses **subnets** for network placement.
- Defines **instance types** and **capacity type** (On-Demand or Spot instances).
- Configures **auto-scaling** with `desired_size`, `min_size`, and `max_size`.
- **Depends on** the IAM policy attachment to ensure permissions are applied.


# Connect to EKS Cluster using AWS CLI and kubectl
# Step 1: Download and Install AWS CLI
Follow the instructions to download and install the AWS CLI from the [official AWS documentation](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html).

# Step 2: Configure AWS CLI
Configure the AWS CLI with your credentials:

```sh
aws configure
```

You will be prompted to enter your AWS Access Key ID, Secret Access Key, region, and output format.

# Step 3: Update kubeconfig with EKS Cluster
Use the following command to update your kubeconfig file with the EKS cluster:

```sh
aws eks --region <your-region> update-kubeconfig --name <your-cluster-name>
```

Replace `<your-region>` with the AWS region where your EKS cluster is located and `<your-cluster-name>` with the name of your EKS cluster.

# Step 4: Verify the Configuration
Verify that your kubeconfig file is correctly configured and you can connect to your EKS cluster by running:

```sh
kubectl get nodes
```

You should see a list of nodes in your EKS cluster.

# Kubernetes Service Account
# What is a Service Account in Kubernetes?
A Service Account in Kubernetes is an identity that pods can use to interact with the Kubernetes API. It provides a way for applications running in pods to authenticate and authorize themselves to perform actions within the cluster.

Service Accounts are important for several reasons:
- **Security**: They provide a secure way for applications to interact with the Kubernetes API without using user credentials.
- **Granular Access Control**: Service Accounts can be assigned specific roles and permissions, allowing fine-grained control over what actions a pod can perform.
- **Isolation**: Different applications or components can use different Service Accounts, ensuring that they only have access to the resources they need.

# Default Service Account
If a user does not specify a Service Account for a pod, Kubernetes automatically assigns the default Service Account in the namespace. This default Service Account has limited permissions and is intended for general use. However, for more secure and controlled access, it is recommended to create and use custom Service Accounts with appropriate roles and permissions.

```yaml
apiVersion: v1
kind: Pod
metadata:
    name: example-pod
spec:
    serviceAccountName: custom-service-account
    containers:
    - name: example-container
        image: example-image
```

In the above example, the `serviceAccountName` field specifies the Service Account to be used by the pod. If this field is omitted, the default Service Account in the namespace will be used.


# Kubernetes Deployment
# What is a Kubernetes Deployment?
A Kubernetes Deployment is a resource object in Kubernetes that provides declarative updates to applications. It allows you to describe an application’s life cycle, such as which images to use for the app, the number of pod replicas, and the update strategy. Deployments manage the creation and scaling of pods, ensuring that the desired state of the application is maintained.

# Kubernetes Deployment vs. Docker Container
# Kubernetes Deployment
- **Declarative Management**: You define the desired state of your application, and Kubernetes ensures that the current state matches the desired state.
- **Scaling**: Easily scale the number of pod replicas up or down.
- **Self-Healing**: Automatically replaces failed or deleted pods to maintain the desired number of replicas.
- **Rolling Updates**: Update applications without downtime by gradually replacing old pods with new ones.

# Docker Container
- **Imperative Management**: You manually start, stop, and manage containers.
- **Scaling**: Requires manual intervention or additional tools to scale containers.
- **Self-Healing**: No built-in self-healing; requires external tools or scripts to handle failures.
- **Updates**: Updating containers often involves stopping the old container and starting a new one, which can lead to downtime.

# Scaling and Healing in Kubernetes
# Scaling
Kubernetes Deployments make scaling applications straightforward. You can scale the number of pod replicas by updating the deployment configuration. Kubernetes will automatically create or remove pods to match the desired replica count.

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
    name: my-app
spec:
    replicas: 3
    selector:
        matchLabels:
            app: my-app
    template:
        metadata:
            labels:
                app: my-app
        spec:
            containers:
            - name: my-app-container
                image: my-app-image:latest
```

# Self-Healing
Kubernetes ensures that the desired state of the application is maintained. If a pod is deleted or fails, the Deployment controller will automatically create a new pod to replace it, ensuring that the specified number of replicas is always running.

```yaml
kubectl delete pod <pod-name>
```

After deleting a pod, Kubernetes will detect the discrepancy and create a new pod to maintain the desired state.

In summary, Kubernetes Deployments provide a robust way to manage applications, offering features like declarative management, scaling, self-healing, and rolling updates, which are not inherently available in Docker containers.


# Kubernetes Services
# What is a Kubernetes Service?

A Kubernetes Service is an abstraction that defines a logical set of Pods and a policy by which to access them. Services enable communication between different components of an application deployed in a Kubernetes cluster. They provide a stable endpoint (IP address and port) for accessing a set of Pods, regardless of their lifecycle.

# How Does It Help with Service Discovery?

In the dynamic environment of Kubernetes, Pods are ephemeral and can be created and destroyed frequently. This makes it challenging to keep track of their IP addresses for communication purposes. Kubernetes Services solve this problem by providing:

1. **Stable Endpoints**: Services provide a consistent IP address and DNS name that remain the same even if the underlying Pods change.
2. **Load Balancing**: Services can distribute traffic across multiple Pods, ensuring high availability and reliability.
3. **Service Discovery**: Kubernetes offers built-in service discovery mechanisms. Pods can discover services using environment variables or DNS.

# Types of Kubernetes Services

1. **ClusterIP**: Exposes the service on an internal IP within the cluster. This is the default type and is used for internal communication between Pods.
2. **NodePort**: Exposes the service on a static port on each node's IP. This allows external traffic to access the service.
3. **LoadBalancer**: Exposes the service externally using a cloud provider's load balancer.
4. **ExternalName**: Maps the service to the contents of the `externalName` field (e.g., a DNS name).

# Example of a Kubernetes Service

```yaml
apiVersion: v1
kind: Service
metadata:
    name: my-service
spec:
    selector:
        app: MyApp
    ports:
        - protocol: TCP
            port: 80
            targetPort: 9376
    type: ClusterIP
```

In this example, the service named `my-service` targets Pods with the label `app: MyApp` and forwards traffic from port 80 to port 9376 on the selected Pods.


# Kubernetes Service Types

Kubernetes services provide a way to expose applications running on a set of Pods as a network service. Kubernetes supports several types of services, each suited to different use cases.

# 1. ClusterIP

# Description
- The default service type.
- Exposes the service on an internal IP in the cluster.
- Makes the service only reachable from within the cluster.

# Use Case
- Suitable for internal services that do not need to be exposed to the outside world.
- Commonly used for communication between microservices within the cluster.

# How It Works
- Kubernetes assigns a stable IP address to the service.
- Pods within the cluster can access the service using this IP address.

# 2. NodePort
# Description
- Exposes the service on each Node's IP at a static port.
- Makes the service accessible from outside the cluster using `<NodeIP>:<NodePort>`.

# Use Case
- Useful for exposing services for external access without a load balancer.
- Suitable for development and testing environments.

# How It Works
- Kubernetes allocates a port from a range (default: 30000-32767) on each Node.
- Traffic to this port is forwarded to the service.

# 3. LoadBalancer
# Description
- Exposes the service externally using a cloud provider's load balancer.
- Automatically creates an external IP address that forwards traffic to the service.

# Use Case
- Ideal for production environments where high availability and scalability are required.
- Suitable for services that need to be accessible from the internet.

# How It Works
- Kubernetes provisions a load balancer from the cloud provider.
- The load balancer distributes incoming traffic across the Pods.

# Conclusion
Choosing the right service type depends on the specific requirements of your application. ClusterIP is best for internal communication, NodePort for simple external access, LoadBalancer for external access.


# Kubernetes: LoadBalancer Service Type vs Ingress
In Kubernetes, both LoadBalancer service type and Ingress are used to expose services to external traffic. However, they serve different purposes and have distinct characteristics. This document explains the differences between the two in detail.

# LoadBalancer Service Type
# Overview
- The LoadBalancer service type is a way to expose a service to external traffic by provisioning an external load balancer.
- It is typically used to expose a single service to the internet.

# Characteristics
- **Automatic Provisioning**: When a LoadBalancer service is created, Kubernetes automatically provisions an external load balancer from the cloud provider.
- **Single Service Exposure**: Each LoadBalancer service exposes a single service.
- **Cloud Provider Dependent**: The implementation and features of the LoadBalancer depend on the cloud provider (e.g., AWS, GCP, Azure).
- **Static IP**: It usually provides a static IP address for the service.

# Use Cases
- Suitable for exposing a single service to the internet.
- Ideal for simple use cases where advanced routing is not required.

# Ingress
# Overview
- Ingress is a Kubernetes resource that manages external access to services within a cluster, typically HTTP and HTTPS.
- It provides more advanced routing capabilities compared to the LoadBalancer service type.

# Characteristics
- **Advanced Routing**: Ingress can route traffic to multiple services based on hostnames, paths, and other rules.
- **Single Entry Point**: It provides a single entry point for multiple services.
- **TLS Termination**: Ingress can handle TLS termination, providing secure HTTPS access.
- **Requires Ingress Controller**: An Ingress resource requires an Ingress controller to be deployed in the cluster (e.g., NGINX, Traefik).

# Use Cases
- Suitable for exposing multiple services through a single IP address.
- Ideal for complex routing scenarios, such as path-based or host-based routing.
- Useful for managing SSL/TLS certificates and providing secure access.

# Comparison Table

| Feature                  | LoadBalancer Service Type | Ingress                       |
|--------------------------|---------------------------|-------------------------------|
| Provisioning            |Automatic by cloud provider| Requires Ingress controller  |
| Service Exposure         | Single service            | Multiple services             |
| Routing Capabilities     | Basic                     | Advanced (host/path-based)    |
| TLS Termination          | No                        | Yes                           |
| Cloud Provider Dependency| Yes                       | No                            |
| Use Case                 | Simple, single service    | Complex, multiple services    |

# Conclusion
Both LoadBalancer service type and Ingress are essential tools in Kubernetes for exposing services to external traffic. The choice between them depends on the specific requirements of your application. Use LoadBalancer for simple, single-service exposure and Ingress for more complex scenarios requiring advanced routing and secure access.


# How to setup alb add on
#  Setup OIDC Connector
# commands to configure IAM OIDC provider 

```
export cluster_name=demo-cluster
```

```
oidc_id=$(aws eks describe-cluster --name $cluster_name --query "cluster.identity.oidc.issuer" --output text | cut -d '/' -f 5) 
```

# Check if there is an IAM OIDC provider configured already
- aws iam list-open-id-connect-providers | grep $oidc_id | cut -d "/" -f4\n 

If not, run the below command

```
eksctl utils associate-iam-oidc-provider --cluster $cluster_name --approve
```

# Download IAM policy
```
curl -O https://raw.githubusercontent.com/kubernetes-sigs/aws-load-balancer-controller/v2.11.0/docs/install/iam_policy.json
```

Create IAM Policy

```
aws iam create-policy \
    --policy-name AWSLoadBalancerControllerIAMPolicy \
    --policy-document file://iam_policy.json
```

Create IAM Role

```
eksctl create iamserviceaccount \
  --cluster=<your-cluster-name> \
  --namespace=kube-system \
  --name=aws-load-balancer-controller \
  --role-name AmazonEKSLoadBalancerControllerRole \
  --attach-policy-arn=arn:aws:iam::<your-aws-account-id>:policy/AWSLoadBalancerControllerIAMPolicy \
  --approve
```

# Deploy ALB controller
Add helm repo

```
helm repo add eks https://aws.github.io/eks-charts
```

Update the repo

```
helm repo update eks
```

Install

```
helm install aws-load-balancer-controller eks/aws-load-balancer-controller \            
  -n kube-system \
  --set clusterName=<your-cluster-name> \
  --set serviceAccount.create=false \
  --set serviceAccount.name=aws-load-balancer-controller \
  --set region=<region> \
  --set vpcId=<your-vpc-id>
```

Verify that the deployments are running.

```
kubectl get deployment -n kube-system aws-load-balancer-controller
```

You might face the issue, unable to see the loadbalancer address while giving k get ing -n robot-shop at the end. To avoid this your **AWSLoadBalancerControllerIAMPolicy** should have the required permissions for elasticloadbalancing:DescribeListenerAttributes.

# Run the following command to retrieve the policy details and look for **elasticloadbalancing:DescribeListenerAttributes** in the policy document.
```
aws iam get-policy-version \
    --policy-arn arn:aws:iam::<your-aws-account-id>:policy/AWSLoadBalancerControllerIAMPolicy \
    --version-id $(aws iam get-policy --policy-arn arn:aws:iam::<your-aws-account-id>:policy/AWSLoadBalancerControllerIAMPolicy --query 'Policy.DefaultVersionId' --output text)
```

If the required permission is missing, update the policy to include it
# Download the current policy
```
aws iam get-policy-version \
    --policy-arn arn:aws:iam::<your-aws-account-id>:policy/AWSLoadBalancerControllerIAMPolicy \
    --version-id $(aws iam get-policy --policy-arn arn:aws:iam::<your-aws-account-id>:policy/AWSLoadBalancerControllerIAMPolicy --query 'Policy.DefaultVersionId' --output text) \
    --query 'PolicyVersion.Document' --output json > policy.json
```
# Edit policy.json to add the missing permissions
```
{
  "Effect": "Allow",
  "Action": "elasticloadbalancing:DescribeListenerAttributes",
  "Resource": "*"
}
```
# Create a new policy version
```
aws iam create-policy-version \
    --policy-arn arn:aws:iam::<your-aws-account-id>:policy/AWSLoadBalancerControllerIAMPolicy \
    --policy-document file://policy.json \
    --set-as-default
```



# Route 53 Hosted Zone
# What is Route 53 Hosted Zone?
Amazon Route 53 is a scalable and highly available Domain Name System (DNS) web service. A hosted zone is a container for records, which include information about how you want to route traffic for a specific domain (such as example.com) and its subdomains.

# Types of Hosted Zones

1. **Public Hosted Zone**: Used to manage the DNS records for a domain that is accessible from the internet.
2. **Private Hosted Zone**: Used to manage the DNS records for a domain that is accessible only from within one or more Amazon VPCs.

# Steps to Create a Hosted Zone

1. **Sign in to the AWS Management Console**:
    - Open the [Route 53 console](https://console.aws.amazon.com/route53/).

2. **Create a Hosted Zone**:
    - In the navigation pane, choose **Hosted zones**.
    - Choose **Create hosted zone**.
    - In the **Create Hosted Zone** pane, enter the following values:
      - **Domain Name**: Enter the name of the domain that you want to route traffic for.
      - **Type**: Choose either **Public Hosted Zone** or **Private Hosted Zone**.
      - **VPC ID**: If you chose **Private Hosted Zone**, select the VPC that you want to associate with the hosted zone.
    - Choose **Create**.


# Update Nameservers for Domain
This sectionwill help in configuringadomain purchased from GoDaddyoratuse AWS Route 53 for DNS management. Specifically, we will set up the domain (for example - `yourdomainname.yourtld`) to route traffic to an AWS Application Load Balancer (ALB) using Route 53.

# Steps
# 1. Create a Hosted Zone in Route 53 [Created in the previous lecture]
1. Open the Route 53 console in the AWS Management Console.
2. Click on `Hosted zones` in the navigation pane.
3. Click on `Create hosted zone`.
4. Enter your domain name (example - `yourdomainname.yourtld`) and select `Public Hosted Zone`.
5. Click on `Create`.

# 2. Update Nameservers in GoDaddy
1. Log in to your GoDaddy account.
2. Navigate to the `My Products` page.
3. Find your domain, example - `yourdomainname.yourtld` and click on `DNS` or `Manage DNS`.
4. Under `Nameservers`, click on `Change`.
5. Select `Enter my own nameservers (advanced)`.
6. Enter the nameservers provided by AWS Route 53. These can be found in the Route 53 console under your hosted zone details.
7. Save the changes.

# 3. Create Record Sets in Route 53
1. In the Route 53 console, select your hosted zone for `yourdomainname.yourtld`.
2. Click on `Create record`.
3. Create an `A` record for `yourdomainname.yourtld`:
    - Name: `www`
    - Type: `A`
    - Alias: `Yes`
    - Alias Target: Select your ALB from the dropdown list.
4. Click on `Create records`.

# 4. Verify the Setup [TAKES UP TO 1-2 days as well]
1. Open a web browser and navigate to `www.yourdomainname.yourtld`.
2. Ensure that the traffic is routed to your AWS ALB and the website loads correctly.