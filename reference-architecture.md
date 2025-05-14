---

# The YAML header is required. For more information about the YAML header, see
# https://test.cloud.ibm.com/docs-internal/writing?topic=writing-reference-architectures

copyright:
  years: 2023
lastupdated: "2025-05-09"

keywords: # Not typically populated

subcollection: pattern-agentic-ai # Use deployable-reference-architectures, or the subcollection value from your toc.yaml file if docs-only.

authors:
  - name: Anuj Jain

# The release that the reference architecture describes
version: 1.0

# Use if the reference architecture has deployable code.
# Value is the URL to land the user in the IBM Cloud catalog details page for the deployable architecture.
# See https://test.cloud.ibm.com/docs/get-coding?topic=get-coding-deploy-button
deployment-url: url

docs: https://cloud.ibm.com/docs/solution-guide

# use-case from 'code' column in
# https://github.ibm.com/digital/taxonomy/blob/main/topics/topics_flat_list.csv
use-case:
  - AIForCustomerService
  - AIGovernance
  - BankingAndFinanceIndustry
  - AIInfrastructureandServers
  - AIPrivacyAndSecurity

# industry from 'code' column in
# https://github.ibm.com/digital/taxonomy/blob/main/industries/industries_flat_list.csv
industry: Banking, FinancialSector, Insurance

# compliance from 'code' column in
# https://github.ibm.com/digital/taxonomy/blob/main/compliance_entities/compliance_entities_flat_list.csv
compliance:

content-type: reference-architecture


# For reference architectures in https://github.com/terraform-ibm-modules only.
# All reference architectures stored in the /reference-architectures directory

# Set production to true to publish the reference architecture to IBM Cloud docs.

production: false

---


{{site.data.keyword.attribute-definition-list}}



# Agentic AI Pattern for watsonx on IBM Cloud
{: #agenticai-pattern}
{: toc-content-type="reference-architecture"}
{: toc-version="1.0"}


This reference architecture summarizes the best practices for deploying agentic artificial intelligence (AI) patterns on IBM Cloud. 

[Agentic AI](https://www.ibm.com/think/insights/agentic-ai) is rapidly enabling a new paradigm for enterprises for improving their products, services, and business processes. Understanding agentic AI and its dependencies is vital for navigating its complex landscape. A production deployment of agentic AI systems requires not just the AI and generative AI capabilities but also has a significant reliance on the traditional supporting services. 

A fundamental architectural decision for agentic AI soultion on IBM Cloud is whether to use a single-tenant or a multi-tenant generative AI platform. 

### Single-tenant generative AI platform

A single-tenant generative AI platform provides a dedicated infrastructure environment on IBM Cloud for AI/gen AI model serving, model management and administration. It is ideal for organizations that need more control over their models and AI workloads with a focus on data sovereignty and compliance needs, security, performance and customization. A single-tenant generative AI platform is hosted within a virtual private cloud (VPC). It aligns with IBM Cloud's best practices and ensures security, high availability, scalability, and optimal performance. The GPU infrastructure is IBM managed and depending on the selected servies on IBM Cloud organization has varying degree of control over generative AI ecosystem.

### Multi-tenant generative AI platform

A multi-tenant generative AI platform logically separates organizations deployments but physically shares the underlying infrastructure environment, managed by IBM Cloud. Multi-tenant genaerative AI platform is available and managed by watsonx.ai SaaS. It provides a more streamlined, fully managed experience and larger ecosystem of products and services for AI/gen AI data and governance. It eliminates the need to manage infrastructure and ecosystem making it suitable for organizations looking for convenience and reduced operational overhead.

Each approach, whether dedicated single-tenant, or shared multi-tenant has its distinct advantages and a decision ultimately depends on the organization's requirements around control, cost, performance, scale, and complexity. More commonly, a hybrid architecture is used - for example consumer may want to host applications using multi-tenant services but use a single-tenant dedicated generative AI platform.

## Architecture diagram
{: #architecture-diagram}

The reference architecture below shows how IBM Cloud provides a secure, compliant and resilient environment to implement an agentic AI system. For single-tenant deployments of applications and generative AI platform the organization (consumer) utilze VPCs with IBM Cloud IaaS and PaaS services. Multi-tenant deployments utilize PaaS and SaaS services. Security, compliance, loggining, monitoring and application lifecycle (devsecops) are common and required services available as SaaS on IBM Cloud. The architecture reuses the [best practices](https://cloud.ibm.com/docs/framework-financial-services?topic=framework-financial-services-about) for IBM Cloud for Financial Services and [VPC reference architecture](https://cloud.ibm.com/docs/framework-financial-services?topic=framework-financial-services-vpc-architecture-about).



** DIAGRAM HERE **

Below is a description about the deployment of workloads and thier administration.

**Management and Administration**<br>

For single-tenant deployment, the Management VPC provides compute, storage, and network services like VPN to enable the consumer's or service provider's administrators to monitor, operate, and maintain the deployed agentic AI environment infrastructure. Multi-tenant deployments utilize IBM Cloud Identiy and Access Management services.

**Application Workload**<br>

For single-tenant deployment, the Application workload VPC provides the dedicated compute, storage, and network services to support the frontend / UI application that end-users use to access an agentic system. It also includes backend applications and business microservices that agentic AI application many require. These include the virtual server instance or Red Hat OpenShift for containerized workloads. For a multi-tenant deployment option will be to use serverless platform like Code Engine for hosting these applications, backend services and IBM Cloud databases. 

**Agentic AI Application Workload**<br>

For single-tenant deployment, the Agentic AI Application Workload VPC provides the dedicated compute, storage, and network services to support the core agentic AI application and their dependencies like the tools and orchestration frameworks. These include the virtual server instance or Red Hat OpenShift for containerized workloads. The multi-tenant option will be to use  serverless platform like Code Engine and other IBM Cloud platforms and services like watsonx.ai and watsonx Orchestrate that provide low-code / no code alternatives to create and host agentic AI systems. 

**Generative AI Platform**<br>

For single-tenant deployment the Gen AI Platform Workload VPC provides the dedicated compute, including GPUs, storage, and network services to securely support a generative AI platform of virtual server instances or containers. The options include:
- Virtual Server Instances (VSI) with GPUs
- Kubernetes cluster with GPU nodes
- Red Hat Enterprise Linux AI (RHELAI) VSI with GPU nodes
- Red Hat Openshift cluster with GPU nodes 
- Red Hat Openshift AI (RHOAI) cluster with GPU nodes
- Red Hat OpenShift Cluster with GPU nodes + watsonx AI software

The available GPUs profiles can be found [here](https://cloud.ibm.com/docs/vpc?topic=vpc-profiles&interface=ui#gpu).

For a multi-tenant option the gen AI capabilities and GPUs are available from watsonx.ai. 

**Edge Compute and Network**<br>

For single-tenant deployments, the edge VPC is used to enhance boundary protection for the end-use facing application workload VPCs, by allowing consumers to access agentic AI user interface and applications through the public internet. Multi-tenant services provide their own security and access controls for the hosted applications and services.

## Design concepts
{: #design-concepts}

Below is the Architecture Framework Design heatmap that covers design considerations and architecture decisions for the following aspects and domains:
* **Data:** Artifical Intelligence
* **Compute:** Virtual Servers, Containers, Serverless
* **Storage:** Primary Storage, Backup
* **Networking:** Enterprise Connectivity, Load Balancing, Domain Name Services
* **Security:** Data Security, Identity & Access, Application Security, Infrastructure & Endpoints, Governance, Risk & Compliance
* **DevOps:** Build & Test, Delivery Pipeline, Code Repository
* **Resiliency:** High Availability
* **Service Management:** Monitoring, Logging, Auditing / tracking, Automated Deployment

![heatmap](heatmap.drawio-v2.svg "Current diagram"){: caption="Figure 3. Architecture design scope" caption-side="bottom"}

## Requirements
{: #requirements}

The following table outlines the requirements that are addressed in this architecture.

| Aspect | Requirements |
| -------------- | -------------- |
| Compute            | Provide properly isolated compute resources with adequate compute capacity for the applications. |
| Storage            | Provide storage that meets the application and database performance requirements. |
| Networking         | Deploy workloads in isolated environment and enforce information flow policies. \n Provide secure, encrypted connectivity to the cloud’s private network for management purposes. \n Distribute incoming application requests across available compute resources. |
| Security           | Ensure all operator actions are executed securely through a bastion host. \n Protect the boundaries of the application against denial-of-service and application-layer attacks. \n Encrypt all application data in transit and at rest to protect from unauthorized disclosure. \n Encrypt all security data (operational and audit logs) to protect from unauthorized disclosure. \n Encrypt all data using customer managed keys to meet regulatory compliance requirements for additional security and customer control. \n Protect secrets through their entire lifecycle and secure them using access control measures. \n Firewalls must be restrictively configured to prevent all traffic, both inbound and outbound, except that which is required, documented, and approved. |
| DevOps            | Delivering software and services at the speed the market demands requires teams to iterate and experiment rapidly. They must deploy new versions frequently, driven by feedback and data. |
| Resiliency         | Support application availability targets and business continuity policies. \n Ensure availability of the application in the event of planned and unplanned outages. \n Backup application data to enable recovery in the event of unplanned outages. \n Provide highly available storage for security data (logs) and backup data. |
| Service Management | Monitor system and application health metrics and logs to detect issues that might impact the availability of the application. \n Generate alerts/notifications about issues that might impact the availability of applications to trigger appropriate responses to minimize down time. \n Monitor audit logs to track changes and detect potential security problems. \n Provide a mechanism to identify and send notifications about issues found in audit logs. |
{: caption="Table 1. Requirements" caption-side="bottom"}

## Components
{: #components}

The following table outlines the products or services used in the architecture for each aspect.

| Aspects | Architecture components | How the component is used |
| -------------- | -------------- | -------------- |
| Data | [Watsonx Assistant](https://www.ibm.com/products/Watsonx-assistant) | Conversational artificial intelligence platform |
|  | [Watson Discovery](https://www.ibm.com/products/watson-discovery) | Automates the discovery of information and insights with advanced Natural Language Processing and Understanding |
|  | [watsonx.ai](https://www.ibm.com/products/watsonx-ai) | Brings together new generative AI capabilities powered by foundation models and traditional machine learning (ML) into a powerful studio spanning the AI lifecycle |
|  | [watsonx.data](https://www.ibm.com/products/watsonx-data) | Enables you to scale analytics and AI with all your data, wherever it resides |
|  | [watsonx.governance](https://www.ibm.com/products/watsonx-governance) | Direct, manage and monitor the artificial intelligence activities |
|  | [Elasticsearch](https://www.ibm.com/topics/elasticsearch) | Database to store vector representations  also known as embeddings created by using machine learning algorithms |
| Compute | [Virtual Servers for VPC](https://cloud.ibm.com/docs/vpc?topic=vpc-about-advanced-virtual-servers&interface=ui) | Web, App, and database servers |
| | [Code Engine](https://cloud.ibm.com/docs/codeengine?topic=codeengine-about) |  Abstracts the operational burden of building, deploying, and managing workloads in Kubernetes so that developers can focus on what matters most to them: the source code|
| | [Red Hat OpenShift Kubernetes Service (ROKS)](https://cloud.ibm.com/docs/openshift?topic=openshift-getting-started) | A managed offering to create your own cluster of compute hosts where you can deploy and manage containerized apps on IBM Cloud |
| Storage | [Cloud Object Storage](https://cloud.ibm.com/docs/cloud-object-storage?topic=cloud-object-storage-about-cloud-object-storage) | Web app static content, backups, logs (application, operational, and audit logs) |
|  | [VPC Block Storage](https://cloud.ibm.com/docs/openshift?topic=openshift-vpc-block) | Web app storage if needed |
| Networking | [VPC Virtual Private Network (VPN)](https://cloud.ibm.com/docs/iaas-vpn?topic=iaas-vpn-getting-started) | Remote access to manage resources in private network |
|  | [Virtual Private Endpoint (VPE)](https://cloud.ibm.com/docs/vpc?topic=vpc-about-vpe) | For private network access to Cloud Services, e.g., Key Protect, COS, etc. |
|  | [VPC Load Balancers](https://cloud.ibm.com/docs/vpc?topic=vpc-load-balancers) | Application Load Balancing for web servers, app servers, and database servers |
|  | [Direct Link 2.0](https://cloud.ibm.com/docs/dl?topic=dl-get-started-with-ibm-cloud-dl) | Seamlessly connect on-premises resources to cloud resources |
|  | [Transit Gateway (TGW)](https://cloud.ibm.com/docs/transit-gateway?topic=transit-gateway-getting-started) | Connects the Workload and Management VPCs within a region
|  | [Cloud Internet Services (CIS)](https://cloud.ibm.com/docs/cis?topic=cis-getting-started) | Global load balancing between regions |
|  | [Access Control List (ACL)](https://cloud.ibm.com/docs/vpc?topic=vpc-using-acls) | To control all incoming and outgoing traffic in Virtual Private Cloud |
| Security | [IAM](https://cloud.ibm.com/docs/account?topic=account-cloudaccess) | IBM Cloud Identity & Access Management |
|  | [Key Protect](https://cloud.ibm.com/docs/key-protect?topic=key-protect-about) | A full-service encryption solution that allows data to be secured and stored in IBM Cloud |
|  | [BYO Bastion Host on VPC VSI](https://cloud.ibm.com/docs/framework-financial-services?topic=framework-financial-services-vpc-architecture-connectivity-bastion-tutorial-teleport) | Remote access with Privileged Access Management |
|  | [App ID](https://cloud.ibm.com/docs/appid?topic=appid-getting-started) | Add authentication to web and mobile apps |
|  | [Secrets Manager](https://cloud.ibm.com/docs/secrets-manager?topic=secrets-manager-getting-started#getting-started) | Certificate and Secrets Management |
|  | [Security and Compliance Center (SCC)](https://cloud.ibm.com/docs/security-compliance?topic=security-compliance-getting-started) | Implement controls for secure data and workload deployments, and assess security and compliance posture |
|  | [Hyper Protect Crypto Services (HPCS)](https://cloud.ibm.com/docs/hs-crypto?topic=hs-crypto-get-started) | Hardware security module (HSM) and Key Management Service |
|  | [Virtual Network Function (VNF)](https://cloud.ibm.com/docs/vpc?topic=vpc-deploy-vnf) | Virtualized network services running on virtual machines. |
| DevOps | [Continuous Integration (CI)](https://cloud.ibm.com/docs/containers?topic=containers-cicd) | 	A pipeline that tests, scans and builds the deployable artifacts from the application repositories |
|  | [Continuous Deployment (CD)](https://cloud.ibm.com/docs/ContinuousDelivery?topic=ContinuousDelivery-getting-started) | A pipeline that generates all of the evidence and change request summary content |
|  | [Continuous Compliance (CC)](https://cloud.ibm.com/docs/devsecops?topic=devsecops-tutorial-cc-toolchain) | A pipeline that continuously scans deployed artifacts and repositories |
|  | [Container Registry](https://cloud.ibm.com/apidocs/container-registry) | Highly available, and scalable private image registry |
| Resiliency | 	[VPC VSIs, VPC Block across multiple zones in two regions](https://cloud.ibm.com/docs/solution-tutorials?topic=solution-tutorials-vpc-multi-region) | Web, app, database high availability and disaster recovery |
| Service Management | [IBM Cloud Monitoring](https://cloud.ibm.com/docs/monitoring?topic=monitoring-about-monitor) | Apps and operational monitoring |
|  | [IBM Log Analysis](https://cloud.ibm.com/docs/log-analysis?topic=log-analysis-getting-started) | Apps and operational logs |
|  | [Activity Tracker Event Routing](https://cloud.ibm.com/docs/activity-tracker?topic=activity-tracker-getting-started) | Audit logs |
{: caption="Table 2. Components" caption-side="bottom"}

## Compliance
{: #compliance}

**CI / CD / CC Pipelines** <br>
The Continuous Integration (CI), Continuous Deployment (CD), and Continuous Compliance (CC) pipelines, referred to as [DevSecOps Application Lifecycle Management](https://cloud.ibm.com/catalog/architecture/deploy-arch-ibm-devsecops-alm-e1c16cac-7ea8-413f-a819-67e3a3251e44-global?catalog_query=aHR0cHM6Ly9jbG91ZC5pYm0uY29tL2NhdGFsb2cjcmVmZXJlbmNlX2FyY2hpdGVjdHVyZQ%3D%3D) are used to deploy the application, check for vulnerabilities, and ensure auditability. Below are some of important compliance features of DevSecOps Application Lifecycle Management: 

* **Vulnerability Scans** <br>
Vulnerability scans involve using specialized tools to look for security vulnerabilities in the code. This is crucial to identify and fix potential security issues before they become a problem in production.

* **Sign Build Artifacts** <br>
The code is compiled and built into software or application artifacts (like executable files or libraries). These artifacts are then digitally signed to ensure their authenticity and integrity.

* **Evidence Gathering** <br>
This involves collecting and storing evidence of the development process, such as commit logs, build logs, and other relevant data. It helps in tracing back and understanding what happened at different stages of development.

* **Evidence Locker** <br>
This involves collecting and storing evidence of the development process, such as commit logs, build logs, and other relevant data. This helps in tracing back and understanding what happened at different stages of development.

**Security and Compliance Center (SCC)** <br>
This reference architecture utilizes the Security and Compliance Center (SCC) which defines policy as code, implements controls for secure data and workload deployments and assess security and compliance posture. For this reference architecture two profiles are used. The [**IBM Cloud Framework for Financial Services**](https://cloud.ibm.com/docs/framework-financial-services-controls?topic=framework-financial-services-controls-overview) and **AI ICT Guardrails**. A profile is a grouping of controls that can be evaluated for compliance.
