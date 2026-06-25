# AD Learning Path 63 — Create an AD Forest Recovery Plan

## Goal
Write and test a forest-recovery runbook covering authority, backups, isolated recovery, restoration order, validation, communications, and return-to-service decisions.

## Prerequisites
- Current AD topology and dependency inventory
- Tested system-state backups
- Recovery time and recovery point objectives
- Isolated exercise environment
- Named technical and business owners

## Plan development
1. Define who may declare a forest recovery and assign the incident, technical, backup, security, and communications roles.
2. List all domains, domain controllers, DNS services, sites, operations-master roles, trusts, service accounts, applications, and identity integrations.
3. Catalogue each trusted backup with date, domain, target, integrity result, and last restore-test date.
4. Define a clean recovery environment using known-good media, isolated networking, protected administration, and independent communications.
5. Document the restoration order: forest-root domain, first writable DC and DNS, required roles, additional domains, additional DCs, sites, and dependent services.
6. Add validation gates for DNS, SYSVOL, time, operations-master ownership, authentication, and replication after every stage.
7. Document which credentials, certificates, trusts, agents, and integrations must be replaced or revalidated.
8. Define evidence handling, progress reporting, exception approval, and return-to-service criteria.
9. Perform a tabletop review and a separate isolated technical exercise.
10. Record gaps, owners, due dates, and a new review date.

## Required sections
```text
Scope and declaration criteria
Roles and contact methods
Forest/domain inventory
Dependency map
Trusted backup catalogue
Isolated recovery prerequisites
Recovery sequence
Validation gates
Credential and certificate actions
Application restoration
Communications and evidence
Return-to-service criteria
Exercise findings
```

## Validation examples
```powershell
Get-ADForest
Get-ADDomain
Get-ADDomainController -Filter *
netdom.exe query fsmo
dcdiag.exe /e
dcdiag.exe /test:DNS /e
repadmin.exe /replsummary
w32tm.exe /monitor
```

## Evidence
Under `evidence/`, store the approved runbook, role assignments, inventory, backup catalogue, restore-test record, tabletop minutes, isolated-lab diagram, stage results, recovery timeline, issues, corrective actions, and final exercise outcome. Keep sensitive recovery material private.

## Success criteria
- A trusted backup can be restored in isolation.
- Approved test users can authenticate.
- DNS, SYSVOL, time, role, and replication checks pass.
- Untrusted systems are not reconnected.
- Timings, gaps, and improvement actions are documented.

## Security notes
Treat forest recovery as a security rebuild. Validate or replace identities and integrations before reconnecting them.

## Cleanup
Dismantle the isolated exercise environment securely after retaining required evidence and updating the plan.

## Next activity
`AD-Learning-Path-64-Capstone-Multi-Site-Enterprise-AD`
