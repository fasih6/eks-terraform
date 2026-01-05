# EKS-Terraform

```mermaid
flowchart TB
    AWS[AWS Cloud<br/>Region: ap-south-1]

    VPC[VPC<br/>10.0.0.0/16]

    subgraph Subnets["Public Subnets"]
        S1[Public Subnet<br/>ap-south-1a]
        S2[Public Subnet<br/>ap-south-1b]
    end

    subgraph Nodes["EKS Worker Nodes"]
        N1[EC2 Node<br/>t2.medium<br/>Pods]
        N2[EC2 Node<br/>t2.medium<br/>Pods]
    end

    CP[EKS Control Plane<br/>(Managed by AWS)]
    IAM[IAM Roles<br/>Cluster & Node Group]
    EBS[EBS CSI Driver<br/>Persistent Storage]
    IGW[Internet Gateway]

    AWS --> VPC
    VPC --> Subnets
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
