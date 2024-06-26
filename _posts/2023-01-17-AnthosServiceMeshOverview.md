---
layout: post
title: Anthos Service Mesh Overview
subtitle: In this blog I provide an overview of the Anthos Service Mesh product offering and architecture, describing how a service mesh helps secure and simplify microservice architectures.
#cover-img: /assets/img/path.jpg
thumbnail-img: /assets/img/anthos/anthoslogo.png
readtime: true
share-title: Anthos Service Mesh Overview
share-description: In this blog I provide an overview of the Anthos Service Mesh product offering and architecture, describing how a service mesh helps secure and simplify microservice architectures.
share-img: /assets/img/anthos/anthoslogo.png
tags: [Anthos Service Mesh, Microservices Architecture, containers, istio, service mesh, app modernisation]
---
  
* toc
{:toc}
 
# Securing Microservices
 
Monolithic applications with multiple functions have no issues communicating internally, but when these applications are modernised and migrate to a microservices architecture, these functions now need to communicate with each other over a network. 
 
![Example monolithic application architecture vs microservice architecture](/assets/img/anthos/monolithvsmicroservice.jpg "Example monolithic application architecture vs microservice architecture")
 
*Example monolithic application architecture vs microservice architecture (source: [CNCF](https://www.cncf.io/blog/2020/02/14/service-mess-to-service-mesh/))*
 
With traditional enterprise networks being secured at the perimeter and providing lateral movement within network segments, organisations need to start treating the network as  an untrusted network and ensure all traffic between functions are authenticated, authorised and securely encrypted. 
 
Building authentication and encryption into each function is a complex and time consuming process. Similarly developers need to consider application performance monitoring (APM) and telemetry for each function, again consuming developer time that could be spent adding business value and improving application business logic. This is where Anthos Service Mesh (ASM) helps. 
 
 ![Anthos Logo](/assets/img/anthos/anthoslogo.png "Anthos Logo")
 
*Anthos Logo (source: [Google Cloud](https://console.cloud.google.com/marketplace/product/google/anthos.googleapis.com
))*
 
# Anthos Service Mesh
The service mesh acts as a layer of infrastructure above the application, managing the network functions and security. It decouples these from the application, running the network functions in a second container within the same pod, as a sidecar envoy proxy (deployed using a sidecar pattern). This enables the application function to communicate with the proxy container as if it was on the same machine. The application has no awareness of this, and becomes truly portable.
 
![Envoy sidecar proxy and traffic flows](/assets/img/anthos/envoyproxy.png "Envoy sidecar proxy and traffic flows")
 
*Envoy sidecar proxy and traffic flows (source [Envoy Proxy](https://www.envoyproxy.io/docs/envoy/latest/intro/life_of_a_request))*
 
Anthos Service Mesh addresses network security, observability and advanced traffic management requirements. Not only does it manage this within a single Kubernetes cluster, the service mesh can run across multiple Kubernetes clusters on the same cloud, across multiple public clouds and even extending to on premise clusters. It enables secure and reliable communication between workloads that may be running on islands of clusters potentially spread around the world.
 
# Anthos Service Mesh Offerings
 
Anthos Service Mesh is a fully managed service mesh based on the open source [Istio project](https://istio.io/). It is available as part of a suite of products under the Anthos platform or individually as a single product offering for teams only requiring the service mesh functionality. 
 
# Anthos Service Mesh Deployment Options
 
Anthos Service Mesh has two deployment options- the first is an in cluster control plane deployment. With this control plane, you install a Google supported distribution of Istio but you are responsible for managing version upgrades, security patches etc. As alluded to in the name of the deployment, the control plane runs within your own cluster.
 
![Anthos Service Mesh In-Cluster Architecture](/assets/img/anthos/anthosservicemeshinclusterarchitecture.svg "Anthos Service Mesh In-Cluster Architecture")
 
*Anthos Service Mesh In-Cluster Architecture (source [Google Cloud](https://cloud.google.com/service-mesh/docs/overview#in-cluster_control_plane))*
 
The second option is a fully managed control plane. With this control plane, you get a fully managed Istio deployment managed and maintained by Google. Google hosts the control plane in a Google managed cluster, separate to your own workload cluster.
 
![Anthos Service Mesh Fully Managed Cluster Architecture](/assets/img/anthos/anthosservicemeshmanagedarchitecture.png "Anthos Service Mesh Fully Managed Cluster Architecture")
 
*Anthos Service Mesh Fully Managed Cluster Architecture (source [Google Cloud](https://cloud.google.com/service-mesh/docs/overview#managed_anthos_service_mesh
))*
 
# The Control Plane
 
The control plane is responsible for managing and configuring the proxies so they are able to route traffic accordingly. The control plane consists of three components.
 
Traffic director: Google Cloud’s fully managed traffic control plane, which is responsible for keeping the proxies up to date with all the service mesh endpoints and directing service mesh ingress and egress traffic.
 
Managed CA: this is the certificate authority responsible for issuing SSL certificates to all the distributed proxies for the purpose of authentication and encryption .
 
Google Cloud Operations: The ingestion point for telemetry, providing monitoring, tracing and logging data for each of the proxies. This tooling also powers the Anthos Service Mesh observability dashboards.
 
# The Data Plane
 
The data plane refers to the envoy proxy sidecar containers that run alongside the application workloads. It is at the data plane that all traffic flows for the workloads are encrypted and authenticated with mutual TLS via the envoy proxies. The proxy manages the traffic flows, as defined and configured and deployed by the control plane.The proxies also collect and report telemetry for mesh traffic.
 
The envoy proxy can be deployed automatically to all workloads within a configured namespace. Any workloads that were running prior to configuring auto deployment of the proxy, will need to be restarted before the sidecar proxy is deployed. 
 
# Network Security
 
Anthos Service Mesh can enforce services to authenticate each other using SSL certificates via mutual TLS (mTLS). With mTLS both the source and destination service authenticate each other, verifying the services are who they claim to be against a certificate issued from a trusted CA. 
 
mTLS also ensures data in transit is encrypted between the services. Where TLS authentication between a client and server validates the server is who the client thinks it is, mTLS ensures the server authenticates the client and they also are who they claim to be. By default, Anthos Service Mesh issues certificates self signed by the mesh CA service that runs on the control plane. In a later blog, I'll cover configuring Anthos Service Mesh with Google Cloud Certificate Authority Service for those scenarios when Mesh CA alone isn’t adequate.
 
mTLS helps mitigate the risk of replay or impersonation attacks of your services from stolen credentials as attackers need access to the services private key in order to impersonate them.
 
Anthos Service Mesh also enables you to restrict access to sensitive services from authorised clients  regardless of the network location or the client and application level credentials e.g. limiting access to a particular GKE namespace, or an authorised service identity. For environments outside of Anthos, IP based access policies can be defined to grant access.
 
Anthos Service Mesh records the identity of the mTLS client and its IP address in logs, enabling you to trace what clients have accessed what resources when, even if the resource was ephemeral.
 
![Mutual TLS Process](/assets/img/anthos/mtlsprocess.png "Mutual TLS Process")
 
*Mutual TLS Process (source [Cloudflare](https://www.cloudflare.com/learning/access-management/what-is-mutual-tls/))*
 
# Observability
 
Anthos Service Mesh provides proactive and reactive observability of services within the mesh. By default, these are integrated with Google Cloud, enabling a centralised single pane of glass dashboard presentation of all Kubernetes clusters within the Google Cloud Console. There are several preconfigured service dashboards in the Google Cloud console so you don't have to manually set up dashboards and charts to observe service behaviour, troubleshoot or optimise your applications.
 
 
![Example Anthos Service Mesh Console View](/assets/img/anthos/servicemeshdashboard.png "Example Anthos Service Mesh Console View")
 
*Example Anthos Service Mesh Console View (source [Google Cloud  Skills Boost](https://www.cloudskillsboost.google/focuses/8459?locale=pl&parent=catalog))*
 
The sidecar proxy intercepts all inbound and outbound HTTP traffic flows and reports them to Anthos Service Mesh providing observability into the health and performance of your workloads. With this feature, developers no longer need to instrument their code to collect telemetry data. The telemetry data is automatically loaded into the Anthos Service Mesh telemetry pages via the Google Cloud Logging and Monitoring API’s.
 
Out of the box Anthos Service Mesh provides 3 of Google’s 4 golden signals for monitoring as per [Google’s Site Reliability Engineering (SRE) practice](https://sre.google/). These include:
 
- Latency: The time it takes to service a request e.g. ms response time of a web page.
- Traffic: A measure of how much demand is being placed on your service e.g. requests per second for a service.
- Errors: The rate of requests that fail e.g. HTTP response 5xx errors.
 
The 4th golden signal is saturation which needs to be manually defined based upon the individual workload and business requirements.
 
From these metrics, Anthos Service Mesh enables you to define SLO’s which can be used to proactively alert support teams before a service impacting issue arises.
 
The console displays all services within the mesh in a services topology graph, records traffic flows that have occurred and provides high level statistics to assess health and performance and drill down into problem areas, simplifying troubleshooting for operations teams. This view shows relationships between services within the mesh, and highlights any flows that are not configured with mutual TLS encryption. 
 
Having a visual representation of known traffic flows also simplifies the impact of future planned maintenance, making it easier to understand the impact an update to a particular service may have on others.
 
![Example Anthos Service Mesh Service Topology Graph](/assets/img/anthos/servicetopology.png "Example Anthos Service Mesh Service Topology Graph")
 
*Example Anthos Service Mesh Service Topology Graph (source [Google Cloud](https://cloud.google.com/service-mesh/docs/observability/explore-dashboard#exploring_the_service_graph))*
 
 
# Advanced Traffic Management
 
Anthos Service Mesh controls the flow of traffic in and out of the service mesh, and between services within the mesh. In addition to this, it provide various traffic management functions including:
 
- Configuring load balancing between services.
- Creating and managing canary or blue/green deployments.
- Creating staged rollouts with percentage based traffic splits.
- Defining circuit breakers, timeouts, retry settings and fault injections.
- Redirecting traffic based on routing rules matching HTTP field attributes.
 
Thanks for taking the time to read this blog, I hope you find it useful and it helps you understand the benefits of Anthos Service Mesh and how it can help overcome some of the issues encountered when adopting a microservices architecture. This is the first of several Anthos blogs I intend to write. In the upcoming blogs I'll be going into more detail and covering deploying, configuring and securing Anthos Service Mesh.
 
Please share, [subscribe](https://www.cloudbabble.co.uk/subscribe) to be alerted to future posts, follow me/connect on [LinkedIn](https://linkedin.com/in/jamiethompson85), and react/comment below!
 
Do reach out if you would like me to cover any particular areas of Google Cloud products, concepts or certifications in future posts.
