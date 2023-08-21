# Elastic-load-balancer
![elb](https://github.com/McTello/Elastic-load-balancer/assets/89931817/624e4b08-c58a-40bf-98a1-a80595267ada)

Short notes on Elastic Load Balancer
# Difference between ALB and NLB

First lets define an Elastic Load Balancer.

Elastic Load Balancing efficiently allocates incoming application traffic among various targets, which can encompass Amazon EC2 instances, containers, and IP addresses, in an automated manner.

Elastic Load Balancing provides fault tolerance for applications by automatically balancing traffic across targets. Targets can be Amazon EC2 instances, containers, IP addresses, and Lambda functions.

ELB distributes traffic across Availability Zones while ensuring only healthy targets receive traffic.

| Feature | Application Load Balancer | Network Load Balancer |
| --- | --- | --- |
| OSI Layer | Layer 7 | Layer 4 |
| Target Type | IP, Instance, Lambda | IP, Instance, ALB |
| Protocols | HTTP, HTTPS | TCP |
| WebSockets | ✔ | ✔ |
| IP addresses as a target | ✔ | ✔ |
| HTTP header-based routing | ✔ |  |
| HTTP/2/gRPC | ✔ |  |
| Configurable idle connection timeout | ✔ |  |
| Cross-zone load balancing | ✔ | ✔ |
| SSL Offloading | ✔ | ✔ |
| Server Name Indication (SNI) | ✔ | ✔ |
| Sticky sessions | ✔ | ✔ |
| Static / Elastic IP Address |  | ✔ |
| Custom Security policies |  |  |

Elastic Load Balancing provides fault tolerance for applications by automatically balancing traffic across targets –

Targets can be Amazon EC2 instances, containers, IP addresses, and Lambda functions.

## Network Load Balancer

The Network Load Balancer (NLB) functions at the level of connections (Layer 4), directing connections to various targets like Amazon EC2 instances, containers, and IP addresses based on IP protocol data.

The NLB is meticulously designed to manage an immense number of requests per second and adeptly handle abrupt spikes in traffic with exceptionally low latencies.

Each Availability Zone can be allocated a single static or Elastic IP address for NLB configuration.

It's possible to balance the load for any application hosted either within AWS or on-premises by utilizing the IP addresses of the application back-ends as targets.

The NLB accommodates connections from clients to IP-based targets even across separate AWS Regions that are peered.

Both network and application target health checks are supported by the NLB.

Long-running and persistent connections, particularly suited for WebSocket applications, are facilitated by the NLB.

NLB offers failover capabilities between IP addresses both within and across AWS Regions, leveraging Amazon Route 53 health checks.

Through integration with Amazon Route 53, it becomes possible to swiftly retire a malfunctioning load balancer IP address from service and redirect traffic to an alternate NLB situated in another region.

While NLB supports cross-zone load balancing, this feature isn't activated by default during the creation of the NLB via the console.

For NLBs, target groups uphold the following protocols and port ranges:

- **Protocols:** TCP, TLS, UDP, TCP_UDP.
- **Ports:** 1-65535.

## Application Load Balancer (ALB)

The Application Load Balancer functions at the level of individual requests (layer 7), intelligently directing traffic to various targets like EC2 instances, containers, and IP addresses, contingent on the content of the request.

It provides the capability to balance the load of HTTP/HTTPS applications while offering specific layer 7 features such as X-Forwarded-For headers.

The ALB offers support for HTTPS termination between clients and the load balancer.

Management of SSL certificates is facilitated by the ALB through AWS IAM and AWS Certificate Manager, utilizing predefined security policies.

With the inclusion of Server Name Indication (SNI), the ALB enables multiple secure websites to share a single secure listener.

By utilizing Server Name Indication (SNI), a client can indicate the specific hostname it intends to connect to.

IP addresses can be configured as targets, allowing load balancing for applications hosted either within AWS or on-premises, utilizing the IP addresses of the backend instances or servers as targets.

For optimal redundancy and availability, a minimum of two Availability Zones are required. Incoming traffic can be evenly distributed across targets in multiple Availability Zones.

The ALB dynamically scales its capacity for handling requests in response to fluctuations in incoming application traffic.

You have the flexibility to configure an ALB to be outward-facing towards the Internet or to create a load balancer devoid of public IP addresses, serving as an internal (non-Internet-facing) load balancer.

Content-based routing is supported by the ALB, enabling the routing of requests to specific services based on the contents of the request. For instance:

- Host-based routing facilitates the routing of client requests based on the Host field of the HTTP header, making it possible to route to multiple domains using the same load balancer.
- Path-based routing directs client requests based on the URL path within the HTTP header (e.g., /images or /orders).
