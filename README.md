# Active Directory IAM Lab
 
## Overview
 
This project demonstrates the design and implementation of an enterprise-style on-premises Identity and Access Management (IAM) environment using Microsoft Active Directory.
 
The environment was built to simulate a small-to-medium business and focuses on secure identity management, role-based access control (RBAC), delegated administration, governance, auditing, least privilege, and separation of duties.
 
The lab implements Microsoft's AGDLP permission model, Access-Based Enumeration (ABE), NTFS permissions, centralized file services, Active Directory redundancy, and a segmented network architecture designed to support secure enterprise operations.
 
---
 
## Project Approach
 
Although this lab is primarily focused on Active Directory and Identity & Access Management (IAM), a significant amount of work was dedicated to planning the underlying infrastructure before implementing identities, permissions, and access controls.
 
Identity systems are only as effective as the environment supporting them. Weak administrative boundaries, poor organizational design, or inadequate segregation of responsibilities can introduce security gaps that undermine IAM controls.
 
For this reason, considerable attention was given to:
 
- Organizational design
- Role design
- Administrative boundaries
- Governance processes
- Access control planning
- Network segmentation planning
- Redundancy planning
 
The objective was not simply to deploy Active Directory, but to design the governance and infrastructure foundation required to operate it securely.
 
> **Note:** The environment was adapted to fit available lab resources. As a result, certain design decisions, including simplified IP schemes, a reduced number of systems, and consolidated server workloads, were made while preserving the core IAM, governance, and security objectives of the project.
 
---
 
## Objectives
 
- Deploy Active Directory Domain Services
- Implement RBAC through AGDLP
- Delegate administrative responsibilities
- Enforce least privilege
- Implement separation of duties
- Configure Access-Based Enumeration (ABE)
- Configure security auditing
- Implement Active Directory redundancy
- Design a segmented enterprise network architecture
 
---
 
## Key Features
 
### Identity & Access Management
 
- Active Directory Domain Services (AD DS)
- Role-Based Access Control (RBAC)
- Microsoft AGDLP Permission Model
- Delegated Administration
- User Lifecycle Management
 
### Security
 
- NTFS Permissions
- Access-Based Enumeration (ABE)
- Password Policies
- Account Lockout Policies
- Security Auditing
- Least Privilege
- Separation of Duties
 
### Governance
 
- Security/GRC Oversight
- Role Change Review Process
- Access Review Model
- Policy Management
- Risk-Based Decision Making
 
### High Availability
 
- DC01 Primary Domain Controller
- DC02 Secondary Domain Controller
- Active Directory Replication
- DNS Redundancy
 
### File Services
 
- Corporate Share
- HR-Finance Share
- Policies
- Logs
- Reports
 
---
 
## Documentation
 
The project has been separated into multiple documents to improve readability and to better represent the planning, implementation, and validation processes behind the environment.
 
| Document | Description |
|-----------|-------------|
| architecture.md | Documents the planned infrastructure, server layout, VLAN design, network segmentation, and access boundaries supporting the IAM environment. |
| design-decisions.md | Explains the reasoning behind architectural, security, governance, and access-control decisions made throughout the project. |
| implementation.md | Details the Active Directory implementation including organizational structure, groups, AGDLP mappings, delegated administration, and resource permissions. |
| validation-testing.md | Contains validation results, security testing, delegated administration verification, redundancy testing, and access control validation. |
 
---
 
## Completed Features
 
- Active Directory Deployment
- Organizational Unit Structure
- Role-Based Access Control (RBAC)
- AGDLP Implementation
- Delegated Administration
- NTFS Permissions
- Access-Based Enumeration (ABE)
- Security Auditing
- Password Policies
- Account Lockout Policies
- Active Directory Replication
- DNS Redundancy
- Domain Controller Redundancy
 
---
 
## Learning Outcomes
 
This project demonstrates practical experience with:
 
- Active Directory Administration
- Identity & Access Management (IAM)
- Role-Based Access Control (RBAC)
- AGDLP Permission Design
- Delegated Administration
- Governance & Compliance
- Security Auditing
- Least Privilege
- Separation of Duties
- High Availability
- Network Segmentation Planning
 
---
 
## Validation Highlights
 
The environment was validated to ensure the implemented controls functioned as intended.
 
Validated controls include:
 
- Delegated Administration
- Role-Based Access Control (RBAC)
- Access-Based Enumeration (ABE)
- Privilege Escalation Prevention
- Audit Logging
- Active Directory Replication
- DNS Redundancy
- Domain Controller Failover
 
Documentation and supporting evidence are available in **validation-testing.md**.
