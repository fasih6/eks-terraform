# EKS-Terraform

```mermaid
flowchart TB
    AWS["AWS Cloud (ap-south-1)"]
    VPC["VPC 10.0.0.0/16"]

    subgraph SUBNETS["Public Subnets"]
        S1["Subnet ap-south-1a"]
        S2["Subnet ap-south-1b"]
    end

    subgraph NODES["EKS Worker Nodes"]
        N1["EC2 Node t2.medium"]
        N2["EC2 Node t2.medium"]
    end

    CP["EKS Control Plane"]
    IAM["IAM Roles"]
    EBS["EBS CSI Driver"]
    IGW["Internet Gateway"]

    AWS --> VPC
    VPC --> SUBNETS

    S1 --> N1
    S2 --> N2

    N1 --> CP
    N2 --> CP

    CP --> IAM
    CP --> EBS

    N1 --> IGW
    N2 --> IGW
```


## Notes 

- The VPC provides isolated networking for the EKS cluster.

- Two public subnets across different AZs ensure high availability.

- EKS Control Plane is fully managed by AWS.

- Worker nodes (EC2) run Kubernetes pods.

- IAM roles provide secure AWS permissions.

- EBS CSI Driver enables persistent storage for Kubernetes workloads.

- Internet Gateway allows nodes to pull container images and updates.
