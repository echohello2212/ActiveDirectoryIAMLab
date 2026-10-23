# Architecture

## Architecture Scope

This project is primarily focused on Identity and Access Management (IAM) rather than network engineering.

Although networking technologies such as VLANs, routing, firewalls, ACLs, and switching were not implemented, the underlying architecture was intentionally designed because secure IAM depends heavily on the surrounding infrastructure.

Weak infrastructure design can lead to governance issues, excessive permissions, poor administrative boundaries, and security weaknesses that undermine IAM controls.

This document describes the planned environment supporting the implemented identity and access management controls.

---

## Domain

```text
adlab.local
```

---

## Network Architecture

```text
                         Internet
                             |
                      Router / Firewall
                  (Inter-VLAN Routing)
                             |
                        Trunk Link
                         (802.1Q)
                             |
                        Core Switch
                             |
 ----------------------------------------------------------------
 |          |          |         |         |          |          |
VLAN 10   VLAN 20   VLAN 30   VLAN 40   VLAN 50   VLAN 60   VLAN 70

Corporate HR/FIN    IT       Mgmt      Servers    GRC      SysAdmin
```

---

## VLAN Summary

| VLAN | Department | Purpose |
|--------|------------|----------|
| VLAN 10 | Corporate | Standard employee workstations |
| VLAN 20 | HR-Finance | Payroll and personnel management |
| VLAN 30 | IT Support | Helpdesk operations |
| VLAN 40 | Management | Leadership and oversight |
| VLAN 50 | Servers | Infrastructure services |
| VLAN 60 | Security/GRC | Information Security, Governance, Risk & Compliance |
| VLAN 70 | SysAdmin | Infrastructure administration |

---

## Planned Traffic Rules

| VLAN | Allowed Access |
|--------|---------------|
| Corporate | Corporate Share, Policies, DNS, Authentication |
| HR-Finance | Corporate Share, HR-Finance Share, Policies, DNS, Authentication |
| IT Support | Corporate user administration and support activities |
| Management | Reports, Corporate Share, Policies |
| Servers | Directory Services, DNS, File Services |
| Security/GRC | Logs, Reports, Policies |
| SysAdmin | Administrative access to all managed infrastructure |

All inter-VLAN communication is expected to traverse a central firewall where access control policies would be enforced.

---

## Server Infrastructure

### DC01

IP Address:

```text
10.0.50.10
```

Roles:

- Active Directory Domain Services
- DNS
- Group Policy
- Authentication

### DC02

IP Address:

```text
10.0.50.11
```

Roles:

- Active Directory Domain Services
- DNS
- Global Catalog
- Replication Partner
- Authentication Redundancy

### DNS Configuration

DC01

```text
Preferred DNS: 10.0.50.11
Alternate DNS: 127.0.0.1
```

DC02

```text
Preferred DNS: 10.0.50.10
Alternate DNS: 127.0.0.1
```

This configuration distributes DNS traffic across both Domain Controllers while maintaining resilience during outages.

### FS01

IP Address:

```text
10.0.50.20
```

Resources:

- Corporate
- HR-Finance
- Policies
- Logs
- Reports

> **Note:** Due to lab resource constraints, file services were hosted on DC01 instead of a dedicated FS01 server.

---

## DHCP

DHCP was intentionally omitted due to the limited scale of the environment.

All systems use static addressing. The primary focus of the project was identity management, governance, access control, auditing, and redundancy.
