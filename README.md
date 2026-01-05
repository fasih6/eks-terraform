# EKS-Terraform

+------------------------------------------------------+
|                    AWS Cloud                         |
|               Region: ap-south-1                     |
+--------------------------+---------------------------+
                           |
                           v
+------------------------------------------------------+
|                        VPC                           |
|                   10.0.0.0/16                        |
+--------------------------+---------------------------+
                           |
        +------------------+------------------+
        |                                     |
        v                                     v
+---------------------------+     +---------------------------+
|      Public Subnet 1      |     |      Public Subnet 2      |
|      ap-south-1a          |     |      ap-south-1b          |
|      10.0.0.0/24          |     |      10.0.1.0/24          |
+------------+--------------+     +--------------+------------+
             |                                   |
             v                                   v
+---------------------------+     +---------------------------+
|   EC2 Worker Node         |     |   EC2 Worker Node         |
|   (t2.medium)             |     |   (t2.medium)             |
|                           |     |                           |
|   +-------------------+   |     |   +-------------------+   |
|   | Kubernetes Pods   |   |     |   | Kubernetes Pods   |   |
|   +-------------------+   |     |   +-------------------+   |
+------------+--------------+     +--------------+------------+
             \                                   /
              \                                 /
               +---------------+---------------+
                               |
                               v
+------------------------------------------------------+
|                EKS Control Plane                     |
|              (AWS Managed Service)                   |
|  - API Server                                        |
|  - Scheduler                                         |
|  - Controller Manager                                |
+--------------------------+---------------------------+
                           |
                           v
+------------------------------------------------------+
|                    IAM Roles                         |
|  - EKS Cluster Role                                  |
|  - EKS Node Group Role                               |
+--------------------------+---------------------------+
                           |
                           v
+------------------------------------------------------+
|                EBS CSI Driver                        |
|        (Persistent Volumes using EBS)                |
+------------------------------------------------------+

+------------------------------------------------------+
|                 Internet Gateway                     |
|        (Outbound internet access for nodes)          |
+------------------------------------------------------+





## Notes 

- The VPC provides isolated networking for the EKS cluster.

- Two public subnets across different AZs ensure high availability.

- EKS Control Plane is fully managed by AWS.

- Worker nodes (EC2) run Kubernetes pods.

- IAM roles provide secure AWS permissions.

- EBS CSI Driver enables persistent storage for Kubernetes workloads.

- Internet Gateway allows nodes to pull container images and updates.
