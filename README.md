# IAM Home Lab — midPoint

An end-to-end Identity Governance (IGA) lab built on **midPoint** (open source), applying the same concepts I support in production on **SailPoint IdentityIQ**: authoritative HR source, provisioning, correlation, Joiner/Mover/Leaver, RBAC, access requests, certifications and SOD.

## Architecture

```
  HR CSV  ──►  midPoint  ──►  OpenLDAP   (directory, stands in for AD)
(source)       (IGA)     ├──► App DB     (internal app, JDBC)
                  │       └──► REST API   (fake SaaS app)
                  ▼
             PostgreSQL (midPoint repository)
```

**Stack:** Docker Desktop (WSL2), midPoint, PostgreSQL, OpenLDAP, Python, Groovy, Java

## Concept mapping: midPoint ↔ SailPoint IIQ

| midPoint | SailPoint IIQ |
|---|---|
| Resource | Application |
| User | Identity |
| Shadow / Projection | Link / Account |
| Import / Reconciliation | Aggregation |
| Correlation | Correlation Rule |
| Groovy script | BeanShell Rule |
| Role | Bundle (Role) |
| Certification campaign | Certification |
| Policy rule | Policy (SOD) |

---

## Progress

### Phase 0 — Lab setup
- [x] Install Docker Desktop + WSL2
- [x] Run midPoint with docker compose and log in
- [x] Create GitHub account
- [x] Change the administrator password
- [x] Install VS Code
- [x] Install Git
- [x] Create this repo and push the lab files

### Phase 1 — HR source (CSV)
- [ ] Build the 100-employee CSV (empId, names, department, title, managerId, status, startDate)
- [ ] Add edge cases: duplicate names, terminated staff, managers
- [ ] Get the CSV into the midPoint container
- [ ] Create the CSV resource as **authoritative** *(IIQ: HR application)*
- [ ] Map HR fields to user attributes *(IIQ: Identity Mappings)*
- [ ] Generate usernames + handle duplicates *(IIQ: Creation Rule)*
- [ ] Import and confirm 100 users created *(IIQ: Aggregation)*
- [ ] Link each user to their manager

### Phase 2 — Directory (OpenLDAP, stands in for AD)
- [ ] Add OpenLDAP to the lab
- [ ] Install Apache Directory Studio and connect
- [ ] Create OU structure + department groups
- [ ] Connect LDAP as a resource in midPoint
- [ ] Provision accounts
- [ ] Manage group membership *(IIQ: Entitlements)*

### Phase 3 — Second app (database)
- [ ] Create app DB with `users` and `user_roles` tables
- [ ] Install DBeaver and connect
- [ ] Connect it as a resource *(IIQ: JDBC connector)*
- [ ] Provision accounts + app roles

### Phase 4 — Correlation & orphans
- [ ] Seed pre-existing accounts (some with slightly different names)
- [ ] Write correlation rules *(IIQ: Correlation Rule)*
- [ ] Handle orphan accounts
- [ ] Run reconciliation and review results

### Phase 5 — Joiner / Mover / Leaver
- [ ] Joiner: new CSV row → accounts created automatically
- [ ] Mover: department change → old access removed, new added
- [ ] Leaver: terminated → disable now, delete later
- [ ] Rehire a terminated employee
- [ ] Manager change on the same day as a move
- [ ] Schedule the HR import task

### Phase 6 — RBAC from scratch
- [ ] Design the role catalog and document it
- [ ] Create IT roles (LDAP groups + app roles)
- [ ] Create business roles containing IT roles
- [ ] Auto-assign roles by department *(IIQ: Assignment rules)*
- [ ] Test that a mover gets the right new roles

### Phase 7 — Access request & approval
- [ ] User requests a role *(IIQ: LCM request)*
- [ ] Manager approval before provisioning
- [ ] Test a rejected request

### Phase 8 — Governance
- [ ] Run a manager access certification campaign
- [ ] Revoke access from a certification decision
- [ ] Create an SOD policy (create payment + approve payment)
- [ ] Trigger a violation and see it caught

### Phase 9 — REST API app & scripting
- [ ] Build a small REST API in Python (fake SaaS app)
- [ ] Connect it as a resource *(IIQ: Web Services connector)*
- [ ] Write Groovy scripts in midPoint *(IIQ: BeanShell rules)*
- [ ] Rewrite the same logic in plain Java

### Phase 10 — Documentation & portfolio
- [ ] HLD document: design decisions and why
- [ ] Architecture + JML diagrams (draw.io)
- [ ] Setup guide + Challenges section
- [ ] 5-minute demo video: joiner → mover → leaver
- [ ] LinkedIn post after each phase

---

## Challenges & lessons learned
*(Filled in as I go: problems I hit and how I solved them.)*

## How to run the lab
*(Setup steps added as each phase is completed.)*

---
> All data in this lab is fictional. Nothing here comes from any employer environment.
