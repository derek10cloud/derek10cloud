# Online subscription support system operation (GKE)

Tool / Platform: GCP, GKE
Work Position: Operating Manager
Period: 2020/06/02

## Objective

- Reliable operation of service
- Operate service securely
- Use various GCP Services

## Achievement

- Reliable operation of service
    - Whenever there's an event traffic can surge dramatically, we operate service flexibly, such as expanding resources (spec up and down)
    - Use GCP's managed services as much as possible, such as Cloud SQL and GKE, to reduce the service failure.
    - Version control with GKE Node Upgrade
- Operate service securely
    - Check for security vulnerabilities and take action
    - Separate IAM Roles between developers and infrastructure managers, managing public-oriented access control through IAP user management
- Use various GCP Services
    - Access GKE Cluster with using Cloud Shell, Cloud SDK
    - CUD(Committed Use Discounts), VM Schedule(VM On/Off)

## What I did

### Proceed below as Operations Manager

### 1. Cloud SQL Instance spec up/down

- Temporarily spec-up DB instances whenever there is an event such as a pre-reservation of phone and down the spec after the event.
- No issues with Spec Up even if CUD is applied to Cloud SQL (temporarily billed on-Demand for only Spec Up capacity)

### 2. Version control with GKE Node Upgrade

- GKE Master automatically upgrade the Kubernetes version (GCP guaranteed)
- We could upgrade a node version automatically or manually, but we wanted to upgrade it when we want to, so we could upgrade the node version manually.
- Proceeded node upgrade with command line such as cordon, drain  ('daemonsets' requires seperate option)

### 3. Check K8S security through the Security Vulnerability Tool

- Delete default namespace, if an engineer runs cluster with default Compute Engine service account, delete the service accounts and make a new one, grant minimum GCR IAM authorization, and so on.

### 4. Authentication, Authorization management using IAP, IAM, etc.

- Role grants based on user's role(Infra, NW, developer) in company (Owner Role is rarely given)
- Control VM access through IAP

### 5. Use GCP Services

- Use the Cloud Shell early, then use the Cloud SDK to access the GKE cluster
- Cost reduction services: Using the contract discount service through CUD, using VM Schedule to automatically turn off emergency VMs outside of business hours