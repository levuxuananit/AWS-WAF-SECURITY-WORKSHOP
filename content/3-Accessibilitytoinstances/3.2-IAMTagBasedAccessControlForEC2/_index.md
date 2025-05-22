---
title : "IAM Tag Based Access Control for EC2"
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 3.2. </b> "
---
### Introduction
This lab will walk you through the steps to configure sample AWS Identity and Access Management (IAM) policies and AWS IAM roles with associated permissions to use EC2 resource tags to control access. Using tags is powerful because it helps you scale your permissions management, but you need to be careful about managing the tags you will learn in this lab.

In this lab, you will create a series of policies attached to a role that an individual such as an EC2 administrator can assume. This allows EC2 administrators to tag resources when they create only if they match requirements and control the existing resources and values ​​they can tag.

The skills you learn will help you protect your workloads according to the AWS Well-Architected Framework.

### Objectives
- Achieve IAM least privilege
- Understand IAM policy requirements

### Best Practices
The security best practices used in this lab are:
- Credential and authentication management: Use MFA for access to provide additional access control.
- Least privilege: Roles are limited to the minimum privileges required to complete the task.
- Prerequisites