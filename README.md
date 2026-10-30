# AWS Cloud Infrastructure & Security Lab

I completed my first AWS infrastructure lab during **Rider University's AWS 101 workshop**, at a CYBHER extracurricular event in October 2026. I used a temporary Workshop Studio account in `us-east-1`, configured the supplied application's infrastructure, and completed the optional Auto Scaling challenge.

**Verified:** 2/2 healthy Auto Scaling instances; 3/3 healthy ALB targets; backends across two Availability Zones. This was a guided console-based workshop, not a production deployment or a custom application I developed.

![Architecture](docs/architecture.svg)

## Explore the project

- [Implementation and security decisions](docs/implementation.md)
- [Validation, limitations and lessons](docs/validation.md)
- [Cleanup and resource lifecycle](docs/cleanup.md)
- [Screenshot evidence index](docs/evidence.md)
- [My portfolio](https://freddyflores.me)

## What I practiced

I separated public-facing load balancing from private compute, used security groups and an IAM instance profile, administered an instance through Systems Manager, worked with S3 and a VPC endpoint, and configured health checks, monitoring, and Auto Scaling. These are foundational skills for understanding cloud exposure, access boundaries and operational resilience in a cybersecurity internship.

## Scope and evidence

I configured infrastructure through the AWS console using workshop instructions, with ChatGPT support for troubleshooting and documentation. This repository documents my work; it is not an infrastructure-as-code deployment or the workshop application source. Selected screenshots are cropped and identifiers are redacted. Raw browser/session captures are not published.

The application used HTTP. Its S3 client returned mock example files according to my lab journal; I do not count that listing as a verified live S3 read. I configured CPU target tracking but did not verify a stress-triggered scaling event. See the validation notes for the full boundaries of the evidence.
