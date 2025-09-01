## Highlights

This project demonstrates how to build a self-healing EC2 workflow on AWS using Ansible roles.
When a new EC2 instance is launched (e.g., by Auto Scaling), it is automatically:

- Bootstrapped with baseline configs (packages, users, timezone).
- Hardened using CIS benchmark rules (SSH lockdown, auditd, sysctl).
- Installed with a CloudWatch monitoring agent.
- Registered with an Application Load Balancer.

## Workflow

- AWS Auto Scaling Group launches EC2 instances.
- Ansible Dynamic Inventory (aws_ec2 plugin) discovers instances automatically.
- Ansible Playbook applies roles:
- common → baseline setup.
- hardening → CIS-compliant configs.
- monitoring → CloudWatch/Datadog agent.
- lb_registration → registers instance with ALB target group.

## Prerequisites

- ansible-galaxy collection install amazon.aws community.aws

## How to run

ansible-playbook -i inventories/aws_ec2.yml playbooks/heal.yml
