# Implementation and security decisions

## 1. Network and entry point

I configured `project-vpc`, public/private subnets, route tables, an Internet Gateway and NAT connectivity. I placed the web server in a private subnet and used an internet-facing Application Load Balancer as its public entry point. This let me practice distinguishing inbound application access from outbound connectivity.

I configured separate security groups for the web server and load balancer. The published capture shows an HTTP inbound rule; its source column is not visible, so this document does not claim an exact source restriction from that capture alone.

## 2. Identity and administration

I created `WebServerInstanceProfile` and attached the Systems Manager managed policy shown in the role screenshot. I opened a Session Manager terminal to the private instance. My journal also records S3 read permission. Using an EC2 role avoids embedding long-lived keys in application files; I did not perform a formal least-privilege policy audit.

In the terminal I checked the private address and the address seen by an external service. The command's label says “Public IPv4 Address,” but that outbound observation should not be mistaken for a public address assigned directly to the private instance.

## 3. Load balancing and storage

I configured `WebServerLoadBalancer` and `WebServerTargetGroup`, with HTTP port 80 targets. I verified the supplied application loaded through the ALB. I created an S3 bucket, uploaded objects, and worked with an S3 VPC endpoint. The journal's mock-client finding limits what the application's S3 interface can prove.

## 4. Optional Auto Scaling challenge

| Setting | My configuration |
| --- | --- |
| Group / template | AutoScalingChallenge / ScalingChallengeTemplate |
| Instance type | t3.micro |
| Availability Zones | us-east-1a and us-east-1b |
| Desired / minimum / maximum | 2 / 2 / 3 |
| Policy | Target tracking, average CPU 50% |
| Policy instance warmup | 300 seconds |
| Default instance warmup | Disabled in the review screen |
| Health checks | EC2 and ELB |
| Health-check grace period | 300 seconds |
| Group monitoring | Enabled |
| Notifications | None for this temporary workshop |

The ASG launched two additional instances. The original server stayed registered, explaining why the ALB had three healthy targets while the ASG had two. I configured a scaling policy, but I did not experimentally verify a CPU-triggered scale-out or a failure-recovery scenario.

## Security relevance

I practiced segmentation, controlled entry, role-based service access, administration without public SSH, service connectivity, health visibility and resource cleanup. Multi-AZ placement and health checks support availability; they do not prove protection against all threats.
