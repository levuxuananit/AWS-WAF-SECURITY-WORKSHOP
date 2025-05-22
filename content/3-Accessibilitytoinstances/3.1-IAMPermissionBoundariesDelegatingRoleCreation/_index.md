---
title : "IAM Permission Boundaries Delegating Role Creation"
date : "`r Sys.Date()`"
weight : 1
chapter : false
pre : " <b> 3.1. </b> "
---
### Introduction
In the Identity and Access Management section, we will walk through the steps to configure sample AWS Identity and Access Management (IAM) permission boundaries. AWS supports permission boundaries for IAM entities (users or roles). Permission boundaries are an advanced feature in which you use managed policies to set the maximum permissions that an identity-based policy can grant to an IAM entity. When you set a permission boundary for an entity, that entity can only perform actions allowed by the policy.

In this section, you will create a series of policies attached to a role that an individual such as a developer can assume, which the developer can then use to create additional user roles that are restricted to specific services and regions. This allows you to delegate access to create IAM roles and policies without exceeding the permissions within the permission boundary. We'll also use a prefixed naming standard, making it easier to control and organize the policies and roles your developers create.