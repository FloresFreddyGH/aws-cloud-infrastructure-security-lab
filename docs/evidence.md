# Screenshot walkthrough

20 selected captures follow my work from setup to cleanup. Open a stage below, then click an image to inspect it at full size. The [short overview](../README.md) and [test limitations](validation.md) provide context.

Browser/account/session headers are cropped out, and sensitive values are masked. These are original screenshots, not generated console images. Setup screens show settings at that moment; success is claimed only where a result confirms it.

## 1. Network setup

<details>
<summary>View 3 screenshots</summary>

### Planning the network

Source capture: `4.png`. I selected two zones, with two public and two private subnets.

![Planning the network](../screenshots/11-vpc-plan.webp)

### Network creation completed

Source capture: `6.png`. The creation workflow confirmed the subnets, routes, Internet Gateway, NAT Gateway and S3 endpoint.

![Network creation completed](../screenshots/12-vpc-created.webp)

### Controlled network access

Source capture: `9.png`. I configured a web-server security group; the capture shows an HTTP inbound rule.

![Controlled network access](../screenshots/01-security-group.webp)

</details>

## 2. Server and access

<details>
<summary>View 3 screenshots</summary>

### Placing the server in a private subnet

Source capture: `15.png`. I disabled automatic public IP assignment and selected the web-server security group. The storage setting shown here was not encrypted; encryption is an improvement for a future build.

![Placing the server in a private subnet](../screenshots/13-private-server.webp)

### An instance role for administration

Source capture: `12.png`. I created WebServerInstanceProfile with the Systems Manager managed policy.

![An instance role for administration](../screenshots/02-instance-role.webp)

### Private instance administration

Source capture: `23.png`. I opened a Systems Manager session. Address values are redacted; the public address check reflects outbound egress.

![Private instance administration](../screenshots/03-session-manager.webp)

</details>

## 3. Load balancing and storage

<details>
<summary>View 2 screenshots</summary>

### Creating the public entry point

Source capture: `30.png`. I selected an internet-facing load balancer and public subnets in both zones.

![Creating the public entry point](../screenshots/14-public-load-balancer.webp)

### Choosing storage settings

Source capture: `41.png`. The bucket creation screen shows versioning disabled and S3-managed encryption selected. This is a settings capture, not a successful application storage test.

![Choosing storage settings](../screenshots/15-storage-settings.webp)

</details>

## 4. Scaling and monitoring

<details>
<summary>View 4 screenshots</summary>

### Saving the server template

Source capture: `48.png`. I created ScalingChallengeTemplate so the scaling group could launch additional servers.

![Saving the server template](../screenshots/16-launch-template.webp)

### Choosing the scaling network

Source capture: `51.png`. I selected the project VPC and its two private subnets for the additional servers.

![Choosing the scaling network](../screenshots/17-scaling-network.webp)

### Capacity and health checks

Source capture: `62.png`. I configured 2 desired instances, a maximum of 3, a 50% CPU target, and EC2/ELB health checks.

![Capacity and health checks](../screenshots/04-scaling-policy.webp)

### Monitoring enabled

Source capture: `63.png`. I enabled group monitoring. The 300-second policy warmup is separate from default instance warmup, which was disabled.

![Monitoring enabled](../screenshots/05-monitoring.webp)

</details>

## 5. Results

<details>
<summary>View 3 screenshots</summary>

### 2/2 Auto Scaling instances healthy

Source capture: `65.png`. I verified that the Auto Scaling group reached its desired capacity.

![2/2 Auto Scaling instances healthy](../screenshots/06-healthy-auto-scaling.webp)

### 3/3 targets healthy across two zones

Source capture: `66.png`. The target group contained the original server plus two Auto Scaling instances, with no unhealthy targets.

![3/3 targets healthy across two zones](../screenshots/07-healthy-targets.webp)

### Application response through the load balancer

Source capture: `68.png`. I verified EC2 connectivity through the application. This capture shows a response from us-east-1a.

![Application response through the load balancer](../screenshots/08-application.webp)

</details>

## 6. Cleanup

<details>
<summary>View 5 screenshots</summary>

### Removing the load balancer

Source capture: `Cleanup 12.png`. The console confirmed deletion and showed no load balancers remaining in the workshop region.

![Removing the load balancer](../screenshots/18-load-balancer-removed.webp)

### Emptying the bucket

Source capture: `Cleanup 20 emptied.png`. The cleanup result shows four objects removed and no failed deletions. This confirms an empty bucket, not final bucket deletion.

![Emptying the bucket](../screenshots/19-bucket-emptied.webp)

### Removing the service endpoint

Source capture: `Cleanup 23.png`. The console confirmed endpoint deletion and showed an empty endpoint list.

![Removing the service endpoint](../screenshots/20-endpoint-removed.webp)

### Project network removed

Source capture: `Cleanup 27.png`. I confirmed deletion of project-vpc and eight associated resources; the default VPC remained.

![Project network removed](../screenshots/09-vpc-cleanup.webp)

### No remaining Elastic IPs in the region

Source capture: `Cleanup 28.png`. I checked the Elastic IP inventory in the workshop region after cleanup.

![No remaining Elastic IPs in the region](../screenshots/10-elastic-ip-check.webp)

</details>
