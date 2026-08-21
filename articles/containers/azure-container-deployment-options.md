Azure Container Deployment Options
Author: faismustafa  
Originally published: February 10, 2023  
Source: Microsoft Community Hub
Overview
The main scope of this blog is to evaluate and understand the capabilities and limitations of Azure container services to help you choose the optimal platform for your container deployments. The container services in scope for this blog are App Service Web App for Containers, Azure Container Instances (ACI), Azure Container Apps (ACA), and Azure Kubernetes Service (AKS). The blog also elaborates on use cases that map well to respective container services and important details learned while evaluating a container service for customer projects/workloads, such as ACA versus AKS.
Different Container Options Available in Azure
App Service Web App for Containers
Azure App Service provides fully managed hosting for web applications, including websites and web APIs. These web applications may be deployed using code or containers. Azure App Service is optimized for web applications. When building web apps, Azure App Service is an ideal option.
Azure Container Instances (ACI)
Azure Container Instances (ACI) provides a single pod of Hyper-V isolated containers on demand. It can be thought of as a lower-level "building block" option compared to Azure Container Apps. Concepts like scale, load balancing, and certificates are not provided with ACI containers. For example, to scale to five container instances/groups, you create five distinct container instances/groups. Azure Container Apps provides many application-specific concepts on top of containers, including certificates, revisions, scale, and environments. Users often interact with Azure Container Instances through other services. For example, Azure Kubernetes Service can layer orchestration and rapidly scale through ACI virtual nodes. If you need a less "opinionated" building block that doesn't align with the scenarios Azure Container Apps is optimizing for, Azure Container Instances is an ideal option. Azure Container Instances is a solution for any scenario that can operate in isolated containers without orchestration. Run event-driven applications, quickly deploy from your container development pipelines, and run data processing and build jobs. It's not made to run indefinitely (24/7), but it's a great way to run a container for a short period of time (e.g., Actions, Jobs, Tasks).
Azure Kubernetes Service (AKS)
Azure Kubernetes Service (AKS) provides a fully managed Kubernetes option in Azure. It supports direct access to the Kubernetes API and runs any Kubernetes workload. The full cluster resides in your subscription, with the cluster configurations and operations within your control and responsibility. For teams looking for a fully managed version of Kubernetes in Azure, Azure Kubernetes Service is an ideal option.
Azure Container Apps (ACA)
Azure Container Apps enables you to build serverless (i.e., no complex infrastructure for you to manage) microservices based on containers. As a serverless solution, it doesn't, however, provide direct access to the underlying Kubernetes APIs. If you require access to the Kubernetes APIs and control plane, you should use Azure Kubernetes Service. However, if you want to build Kubernetes-style applications and don't require direct access to all the native Kubernetes APIs and cluster management, Azure Container Apps provides a fully managed experience based on best practices. For these reasons, many teams may prefer to start building container microservices with Azure Container Apps.
Azure Container Apps Use Cases
Deploy and manage a microservices architecture with the option to integrate with Dapr (an open source API that takes care of complex challenges such as service discovery, message broker integration, encryption, observability, and secret management).
Event-driven processing such as a queue reader application that processes messages as they arrive in a queue.
Web Applications such as ASP.NET Core, Express.js with custom domains, TLS certificates, with integrated authentication.
Public API endpoints that split traffic between two revisions of the app.
Background processing that, for example, continuously runs a background process transforming data in a database.
What can you do with Azure Container Apps?
Run multiple container revisions and manage the container app's application lifecycle.
Autoscale your apps based on any KEDA-supported scale trigger. Most applications can scale to zero.
Enable HTTPS ingress without having to manage other Azure infrastructure.
Split traffic across multiple versions of an application for Blue/Green deployments and A/B testing scenarios.
Use internal ingress and service discovery for secure internal-only endpoints with built-in DNS-based service discovery.
Build microservices with DAPR and access its rich set of APIs.
Run containers from any registry, public or private, including Docker Hub and Azure Container Registry (ACR).
Use the Azure CLI extension or ARM templates to manage your applications.
Securely manage secrets directly in your application.
View application logs using Azure Log Analytics.
Container Services Comparison
				
Azure Container Services	Use Case	Benefits	Limitations	Architecture References
Azure Container Apps	- Serverless container platform for building modern apps and stateless microservices workloads on Linux without dealing with any infrastructure or container orchestrator and additional AKS functionality not needed. - Good for someone who needs to containerize and get simple benefits of AKS without dealing with the complexity.	- Optimized for running general-purpose containers, especially for applications that span many microservices deployed in containers - Powered by Kubernetes, Dapr, KEDA, and envoy - Supports Kubernetes-style apps and microservices with features like service discovery and traffic splitting - Scaling based on traffic and pulling from event sources like queues - Supports scale to zero  - Support for long-running processes and can run background tasks	- No direct access to underlying Kubernetes APIs.  - No access to broader CNCF projects  - App memory and CPU resource allocation ranges are limited.	Deploy microservices with Azure Container Apps
Azure Kubernetes Service	- Complex and distributed applications where you need to have more control and make efficient use of infrastructure resources. Run containers at scale with flexible networking and customization options.	- Container orchestration for automating deployment, scaling, and management - Auto healing - Support for CNCF Projects Like Istio, Flux, Argo DAPR and KEDA support - Uses node pools and pods to scale and deploy applications - Elastic provisioning	- Infrastructure, network, and VM management - High Learning Curve - User responsibility for updates and upgrades - Complex Developer Experience - Certificate and Secret management - Complex troubleshooting	Microservices architecture on Azure Kubernetes Service  Advanced AKS microservices architecture  Azure Kubernetes in event stream processing
Azure Container Instances	- Simple and serverless applications with more predictable usage patterns. You can integrate it with AKS to scale out more quickly.	- Ease of use. - Fast container start. - Custom sizing. - No need for full orchestration. - Ideal for simple container-based workloads. - Great for monolithic workloads such as Actions, Jobs, and Tasks.	- No Orchestration (Kubernetes) - Not suitable for running large-scale applications. - No service discovery. - No support for Scaling.	
App Service Web App for Containers	- Run containerized web applications without managing any infrastructure.	- Deploy to Azure in seconds. - Deploy code or containers. - Scale easily on demand. - Ideal for web applications. - Leverage Deployment slots to minimize downtime.  - Managed certificates	- Docker Compose is supported in preview. - No DAPR (Distributed Application Runtime). - No event-driven processing Using KEDA (Kubernetes Event-driven Autoscaler).	Lift and shift to containers with Azure App Service
App Service Web App for Containers and Azure Container Apps Comparison
Please note that Azure Container Instances is not covered in the table below because it is not an orchestrator and is primarily intended for simpler workloads such as actions, jobs, and tasks.
Use Cases
	
ACA	App Service Web App for Containers
- Serverless container platform for building modern apps and microservices(container apps are defined by container images)	- Highly reliable PaaS solution for both code (App Service) and containers (App Service Web App for Containers)
- Communication between container apps in the same ACA environment (deploy different applications to the same virtual network)	- Apps in the same App Service Plan by default cannot communicate with each other directly (traffic will need to go outside of the plan first)
- Native Azure monitor integration. - No support for log / metric shipping capability to third-party tools	- Rich out-of-the-box logging - Infrastructure/platform logs - Can be integrated with App Insights for application logs
- One ACA environment can host multiple Apps	- One App Service Plan could host multiple apps
- API endpoints - Handling event-driven processing - Background processing applications - Running Microservices	- Web apps - API endpoints
Feature Comparison of App Service Web App for Containers, ACA, AKS
			
	ACA	App Service Web App for Containers	AKS
Best Candidates	- API - Web apps/Microservices - Background processing applications - Event-driven processing	- API - Web Apps - Deploying long-running containers/services	- API - Lift and Shift to Containers/Microservices - Event-driven processing - IoT Applications - Ease of scaling with ACI
Architecture	- ACA is a new serverless container platform for building modern apps and microservices, built on a foundation of AKS, KEDA, DAPR, and Envoy. ACA gives you the benefits of running containers while leaving behind the concerns of managing cloud infrastructure and complex container orchestrators. Supports Ingress without the need to set up underlying infrastructure like Azure LB or Public IP - Bind one or more custom domains to a container app.  - Supports TLS termination.  - As a PaaS service (unlike AKS), also fully managed by Microsoft.	- App Service Web App for Containers is a PaaS service and could host Apps for multiple frameworks and languages. - Web App gets out-of-box built-in support for Health check, Log Aggregation, Load Balancer, etc. - Custom Domain support - TLS setup integrated with AKV – Out of box Web Apps provide a fully managed environment with nodes and framework runtimes fully patched and updated.  - Customer manages application code only.	- AKS is a managed (not PaaS) Kubernetes service in Azure. The control plane of an AKS cluster is managed by Azure, which offloads significant operational overhead from you as an AKS customer. However, unlike other Azure PaaS services such as App Service, keeping an AKS cluster up and running is a shared responsibility between you and Azure.
Deployment	- Deploy Containers (currently only Linux)	- Deploy Code or Containers (either Windows or Linux).	- Deploy Containers (either Windows or Linux).
Orchestration	- A revision is an immutable snapshot of a container app - A container app can have multiple revisions - Combined with Ingress, can be used for typical traffic direction strategies, including A/B testing and Blue/Green deployment.	- Has built-in deployment strategies – Blue/Green deployment, canary deployment, and traffic splitting using deployment slots - Keep alive and self-healing	- Ingress controllers, Service Mesh, and some Open Source tools do provide deployment strategies.
Scaling	- Out of box Transparent HPA - Max replicas limited to 30 - Native KEDA integration – A variety of metrics - Autoscaling – Scale based on HTTP requests, events, or run always-on background jobs	- Web Apps on App Service Environment (ASE) support vertical and Horizontal scaling, but all applications residing on the same plan will get the same-sized Nodes. - Scale up – change App Plan - Scale-out – increase instances - Autoscaling supported on Azure Monitor metrics	- Out of the box with metrics server in combination with HPA. - Cluster AutoScaler - Scaling limited to CPU/Memory - Apps can be scaled to X number of pods.
Monitoring	- Azure Monitor for out-of-the-box metrics, logs, and alerts - Use Application Insights to monitor the code in ACA. ACA doesn't support Application Insights auto-instrumentation agent, but you can instrument your application code using Application Insights SDKs. - No support for log / metric shipping capability to third-party tools	- Out of the box App Insights and Azure Monitor  - Bring your own Logging/Monitoring could be integrated with many providers	- Native Azure monitor integration. - Container insights. - Application Insights. - Prometheus and Grafana - Logs/Metrics can be shipped to third-party tools such as Splunk and Sumologic.
Security & Identity	- Azure IAM RBAC - MSI can be enabled to access other resources (access to ACR still needs admin enabled) - Currently(2022.11) no native integration to AKV, secret management limited to key-value pairs - Currently(2022.11) no runtime portion (DfC in the roadmap) -HTTPS endpoint by default. mTLS with Dapr Out of the box	- Azure IAM RBAC - MSI enabled to secure access to Azure resources. - Application AAD integration Out of the box with EasyAuth plugin	- Azure and Kubernetes RBAC - Supports Managed identities. - Workload identity for applications. - Secret management via CSI driver and Key Vault or can be integrated with external secret management tools such as Hashicorp vault. - Flexibility in exposing ports for pods. - No Out of the box mTLS support for pods. - Azure defender for containers is supported.
Networking	- Can be integrated with VNets (public or private or none endpoints) - Out-of-the-box Azure CNI abstracted from the user. Can be fully isolated via the Azure container environment.	- App Service (premium tier) with Private Link and VNet integration AppService Environment is also a fully isolated and private network.	- Supports VNet integration - Flexibility in managing IP addresses. - Network policies to isolate pods within the cluster. - Supports different ingress controllers.
SLA	- We guarantee that Apps running in a customer subscription will be available 99.95% of the time.	- We guarantee that Apps running in a customer subscription will be available 99.95% of the time. - No SLA is provided for Apps under either the Free or Shared tiers.	Control Plane Uptime SLA:   --99.95% - if the availability zone is selected. -- 99.9% within the region.  Application/Node SLA:  -- 99.99% across availability zones  -- 99.95% within single region/zone
Learnings from customer projects that highlight ACA and AKS limitations/benefits
When working with customers, it is essential to clearly state that Azure Container Apps are not a replacement for AKS. It is worthwhile to cover the main use cases that Azure Container Apps are designed for:
Microservices: Deploy and manage a microservices architecture with the option to integrate with Dapr
Event-driven processing: Queue reader application that processes messages as they arrive in a queue
Web Applications: Deploy and mage web apps with custom domains, TLS, certificates, integrated authentication
Public API endpoints: HTTP requests are split between two revisions of the app, e.g., the first revision gets 80% of the traffic, new revision receives 20%
Background processing: E.g., continuously-running background process that transforms data in a database
Another aspect to clearly state is though the underlying infrastructure consists of AKS clusters that support Container Apps, there is no access to the AKS clusters and, thus, the Kubernetes APIs. AKS is a managed service, and access to the AKS cluster is possible.
One of the major factors to consider when choosing between ACA and AKS is scaling. You must understand the scaling requirements of your workload. At the moment, ACA only scales to 30 replicas. This is a soft limit and can be increased by calling support per subscription. However, we have experienced customer workloads that required scaling to 50-70 nodes and upwards of 500 replicas. Even though ACA was the perfect platform for the use case, including background mathematical calculations and reading messages from a service bus queue, the scaling requirements were met by AKS but not by ACA.
Please refer to Quotas for Azure Container Apps concerning Environments, Container Apps, Revisions, Replicas, and Cores (these are soft limits and can be increased by contacting Azure Support).
One interesting observation we noticed while benchmarking the actual scaling performance was that the underlying nodes in ACA could scale to accommodate more replicas faster than the nodes that scaled on AKS.
In ACA, the current consumption tier is the shared tenant model, and this does not have support for UDR support. This feature is planned for a premium tier that will be in preview in the future. So when designing your architecture for ACA and UDR support is needed, you may need to consider AKS currently.
Out of the box, ACA comes with KEDA, Dapr, and ENVOY deployed. So one can use Dapr for microservices using Dapr APIs, and use KEDA to scale your applications by specifying scaling criteria in your ARM templates or the Azure portal. In the case of AKS, one must go through a sequence of steps to get these set up.
Observability is, of course, very important for customers to monitor their applications deployed to ACA or AKS. It is essential to note the observability constraints of ACA. The following metrics can be monitored in ACA:
CPU Usage
Memory
Network in/out
Requests
Replica Count
Replica Restart Count
Please also note these observability constraints of ACA:
App and System (ACA environment) logging
Live streaming
Troubleshooting on console
Azure Monitor Metrics
Within AKS, there is more flexibility when it comes to Observability:
Container Insights
Prometheus and Grafana
Following are Operational Activities in AKS that need not apply to ACA:
AKS Day-2 - Patch and upgrade guidance
Node Image updates
Handle Linux node reboots with kured
Cluster Version upgrades.
Cluster Authentication:
Use Azure AD in Azure Kubernetes Service
Limit access to kubeconfig in Azure Kubernetes Service (AKS)
Ensure you're not leveraging deprecated k8s API version with new Kubernetes version. Kubernetes Release Notes
You need to configure hardware (nodePool) autoscaling in addition to app-specific autoscaling. Concepts - Scale applications in Azure Kubernetes Services (AKS)
