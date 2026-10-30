# Cleanup

I intentionally decommissioned the temporary workshop infrastructure after testing. My cleanup sequence included:

1. Delete the Auto Scaling group and launch template.
2. Terminate all three EC2 instances.
3. Delete the ALB and target group, then the two workshop security groups.
4. Empty the S3 bucket and remove the S3 VPC endpoint.
5. Initiate and monitor NAT Gateway deletion.
6. Delete project-vpc and its associated resources.
7. Check the Elastic IP inventory in us-east-1.

The selected evidence explicitly confirms deletion of **project-vpc and eight associated resources**, and **no allocated Elastic IPs in the region**. The default VPC remained. The raw sequence includes the bucket-deletion dialog, but not independent confirmation of final bucket deletion. This was not an all-regions resource audit.

Cleanup was part of the exercise: removing unused infrastructure reduces abandoned exposure and unnecessary resource consumption. The former workshop endpoint is not offered as a live demo.
