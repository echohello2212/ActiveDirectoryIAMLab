# Design Decisions

## Why AGDLP?

The environment utilizes Microsoft's recommended AGDLP model:

Accounts ↓ Global Groups ↓ Domain Local Groups ↓ Permissions

Users are assigned to Global Groups based on their job role or department. Global Groups are then linked to Domain Local Groups, which act as permission containers for specific resources. Permissions are assigned to the Domain Local Groups rather than directly to users, allowing access to be managed through group membership.

Example:

William Bee ↓ GG_Corporate ↓ DL_Corporate_RW ↓ Corporate Share

This approach simplifies permission management, supports Role-Based Access Control (RBAC), and reduces administrative overhead when users change roles or leave the organization.

```text
Accounts
    ↓
Global Groups
    ↓
Domain Local Groups
    ↓
Permissions
```

Benefits include:

- Simplified permission management
- Easier onboarding and offboarding
- Reduced administrative overhead
- Scalable RBAC implementation

---

## Why Everyone Belongs to GG_Corporate?

Every employee requires access to common organizational resources.

Examples include:

- Corporate Share
- Policies
- General company resources

For this reason all users inherit membership in:

```text
GG_Corporate
```

This provides a baseline level of organizational access while department-specific permissions are assigned through additional Global Groups.

---

## Why SysAdmins Also Have IT Support Access?

SysAdmins retain all IT Support capabilities while maintaining responsibility for infrastructure administration.

This allows SysAdmins to perform:

- User creation
- User deletion
- Password resets
- Account unlocks

while also managing:

- Active Directory
- DNS
- Group Policy
- Infrastructure services

This reflects a realistic enterprise environment where senior administrators often retain support capabilities while maintaining broader infrastructure responsibilities.

---

## Why Restrict IT Support?

IT Support is intentionally limited to delegated user administration.

### Allowed

- User creation within delegated scope
- Password resets
- Account unlocks
- Viewing user information

### Denied

- User deletion
- Role assignment
- Group management
- Infrastructure administration

This reduces attack surface and limits the impact of mistakes or misuse.

More privileged identity operations remain the responsibility of SysAdmins due to the potential impact on security, governance, and business operations.

---

## Why SysAdmins Control Role Assignment?

Role changes directly affect access to sensitive resources.

Examples include:

```text
Corporate → HR-Finance
Corporate → Management
IT Support → Management
```

Because role assignments determine access to sensitive business data and resources, these changes are treated as privileged actions.

For this reason, role assignment remains a SysAdmin responsibility.

---

## Why HR and Finance Are Combined?

In larger organizations, Human Resources and Finance would typically operate as separate departments.

For the scope of this lab they were combined because both functions manage highly sensitive employee and financial information.

Responsibilities include:

- Payroll
- Compensation
- Personnel records
- Employee onboarding and offboarding
- Employment documentation
- Benefits administration

Combining these functions reduced administrative complexity while still allowing implementation of appropriate access controls.

In a larger environment these functions would likely be separated to further strengthen segregation of duties.

---

## Why Security and GRC Are Combined?

Security/GRC combines:

- Information Security
- Governance
- Risk Management
- Compliance

In larger organizations these functions frequently exist as separate departments.

For the scope of this lab they were combined to reduce complexity while still demonstrating governance, oversight, compliance, and risk management processes.

This allows the project to include governance concepts without unnecessarily increasing organizational complexity.

---

## Security/GRC Responsibilities

The Security/GRC department provides independent oversight of the environment.

Although much of their work is less visible within the technical implementation of the lab, they play a critical role in ensuring controls remain effective and aligned with business requirements.

Responsibilities include:

- Access reviews
- Audit reviews
- Compliance validation
- Risk assessments
- Policy oversight
- Change approvals

Security/GRC evaluates decisions based on:

- Business risk
- Security impact
- Internal policies
- Compliance obligations
- Regulatory requirements

Unlike SysAdmins, Security/GRC personnel do not administer infrastructure.

Their primary responsibility is ensuring that access, permissions, and administrative changes remain aligned with organizational requirements and acceptable levels of risk.

---

## Why Security/GRC Reviews Role and Permission Changes?

Role assignments and permission changes can significantly impact security and compliance.

Examples include:

- Access to payroll information
- Access to management reports
- Access to audit information
- Assignment of elevated privileges

For this reason, Security/GRC provides oversight of significant access changes to ensure they remain compliant with organizational requirements and acceptable risk levels.

This separation helps ensure that the team implementing changes is not also responsible for approving them.

---

## Why HR-Finance and Security/GRC Can Modify Policies?

Both departments contribute directly to organizational policy development.

### HR-Finance

Responsible for:

- Employee handbooks
- Personnel policies
- Codes of conduct
- Workplace standards

### Security/GRC

Responsible for:

- Security policies
- Governance standards
- Compliance controls
- Risk management requirements

Because both teams contribute to policy creation and maintenance, both require read/write access to the Policies repository.

---

## Why Restrict Log Access?

Permissions:

```text
IT Support     = Write
SysAdmin       = Write
Security/GRC   = Read
Everyone Else  = No Access
```

Operational teams submit logs while Security/GRC independently reviews audit information.

This model creates a clear separation between the producers of audit data and those responsible for reviewing it.

Benefits include:

- Improved audit integrity
- Reduced opportunity for tampering
- Stronger separation of duties
- Independent oversight

---

## Why Security/GRC Owns Reports?

Permissions:

```text
Security/GRC = Read/Write
Management   = Read
HR-Finance   = Read
```

Security/GRC creates and maintains:

- Audit reports
- Compliance reports
- Governance reports
- Risk reports

HR-Finance receives read access to reports containing employee-related information, including compensation, personnel matters, and conduct violations.

Management receives read access to support business oversight and decision-making.

Security/GRC retains ownership of report creation and management.

---

## Why Access-Based Enumeration?

Access-Based Enumeration (ABE) ensures users only see resources they are authorized to access.

Benefits include:

- Reduced information disclosure
- Improved security
- Cleaner user experience
- Reduced user confusion

Users are prevented from viewing folders and shares for which they have no permissions.

This supports the principle of least privilege while improving usability.

---

## Why Deploy DC02?

DC02 removes the single point of failure represented by DC01.

Benefits include:

- Authentication redundancy
- DNS redundancy
- Active Directory replication
- Higher availability
- Improved fault tolerance

This design ensures authentication and directory services remain available during planned maintenance or unexpected outages affecting a single Domain Controller.

---

## Why Configure Domain Controllers to Use Each Other for DNS?

Active Directory relies heavily on DNS for authentication, service discovery, and replication.

For this reason:

```text
DC01
    ↓
Preferred DNS
    ↓
DC02

DC02
    ↓
Preferred DNS
    ↓
DC01
```

Benefits include:

- DNS redundancy
- Improved resilience
- Reduced dependency on a single server
- Continued name resolution during outages
This configuration was validated by successfully authenticating users after shutting down DC01 and relying on DC02 for both authentication and DNS services.
