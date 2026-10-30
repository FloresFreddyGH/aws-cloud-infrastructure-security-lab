# Validation and lessons

| Check | Evidence / outcome |
| --- | --- |
| ASG desired capacity | Screenshot 65: at desired capacity, 2 instances, 2/2 healthy |
| ALB target health | Screenshot 66: 3 healthy, 0 unhealthy, across us-east-1a and us-east-1b |
| Application EC2 connection | Screenshot 68: explicitly successful, responding in us-east-1a |
| Cross-zone responses | My supplied workshop summary records responses in both zones; the selected application capture shows zone A, while target health independently shows both zones |
| S3 | Objects uploaded according to my journal; application listing used a mock S3Client, not proof of a live read |
| External API | Interface reached; successful API response not established |
| CPU scaling | Policy configured; no stress test or observed scale-out to 3 ASG instances |

## What I learned

I learned to follow traffic from the public ALB to private compute and distinguish role permissions, network paths, application behavior and console health. A green health check answers a narrow question; it is not a security assessment. A visible file list also is not enough to verify S3 integration when the application returns mock data.

## Future improvements — not completed in this lab

- Configure TLS and an HTTPS listener; the workshop used HTTP.
- Review IAM policies and security-group sources for least privilege.
- Add appropriate CloudTrail, VPC and ALB logs for audit and investigation.
- Run controlled scaling and recovery tests.
- Rebuild with Terraform or CloudFormation for repeatability.

I do not claim throughput, uptime benchmarks, penetration testing, threat hunting or a production security audit.
