# Skyline GUI Documentation Migration Plan

## Objective
Rewrite all Dashboard tab content in docs to match actual Skyline console UI — exact form fields, menu paths, list columns, actions, and detail pages cross-validated against code.

## Status Tracking
- DONE = Code read, docs rewritten, review passed
- IN PROGRESS = Currently being worked on
- PENDING = Not started

---

## Completed

| Phase | Service | Pages | Status |
|-------|---------|-------|--------|
| — | Key Manager (Barbican) | 3 | DONE |
| — | DNS (Designate) | 5 | DONE |
| — | Instance HA (Masakari) | 5 | DONE |
| | **Total Done** | **13** | |

---

## Phase 1: Core User Services (69 pages)

These services appear in BOTH the user and admin Skyline menus. Highest customer visibility.

### P1-A: Compute (18 pages) — PRIORITY 1
**Skyline menu**: Compute > Instances, Flavors, Server Groups, Images, Key Pairs, Instance Snapshots
**Skyline code**: `src/pages/compute/containers/Instance/`, `Flavor/`, `ServerGroup/`, `Image/`, `Keypair/`, `InstanceSnapshot/`
**Admin-only extras**: Hypervisors, Host Aggregates, Bare Metal Nodes (ironic endpoint)

Pages to rewrite:
```
services/compute/launch-instance.mdx          ← Instance Create wizard (biggest form in Skyline)
services/compute/resize-instance.mdx          ← Resize action
services/compute/reboot-instance.mdx          ← Reboot/hard-reboot actions
services/compute/rescue-instance.mdx          ← Rescue action
services/compute/snapshots.mdx                ← Create snapshot action
services/compute/manage-ips.mdx               ← Floating IP attach/detach
services/compute/security-groups.mdx          ← Security group assignment
services/compute/server-groups.mdx            ← ServerGroup create form
services/compute/block-device-mapping.mdx     ← Part of launch wizard
services/compute/console-access.mdx           ← Console action (VNC/SPICE)
services/compute/availability-zones.mdx       ← AZ selection in launch
services/compute/flavors.mdx                  ← Admin: Flavor create form
services/compute/quotas.mdx                   ← Admin: Quota management
services/compute/compute-hosts.mdx            ← Admin: Hypervisors list
services/compute/scheduling.mdx               ← Admin: Host aggregates
services/compute/live-migration.mdx           ← Admin: Migrate action
services/compute/live-resize-admin.mdx        ← Admin: Live resize
services/compute/bare-metal.mdx               ← Admin: Ironic bare metal nodes
```

**Method**: 
1. Launch explorer agent to read ALL Instance/actions/*.jsx (Create wizard is multi-step), Flavor/actions/*, ServerGroup/actions/*
2. Rewrite each page with exact Skyline form fields
3. Run /review-docs compute

### P1-B: Block Storage (17 pages) — PRIORITY 2
**Skyline menu**: Storage > Volumes, Volume Backups, Volume Snapshots, Volume Types (admin), Storage Backends (admin)
**Skyline code**: `src/pages/storage/containers/Volume/`, `Backup/`, `Snapshot/`, `VolumeType/`, `Storage/`

Pages to rewrite:
```
services/storage/create-volume.mdx            ← Volume Create form
services/storage/attach-volume.mdx            ← Attach action
services/storage/extend-volume.mdx            ← Extend action
services/storage/snapshots.mdx                ← Snapshot create
services/storage/backups.mdx                  ← Backup create/restore
services/storage/volume-transfers.mdx         ← Transfer create/accept
services/storage/volume-types.mdx             ← User: view types
services/storage/volume-types-admin.mdx       ← Admin: create/manage types
services/storage/qos.mdx                      ← Admin: QoS specs
services/storage/quotas.mdx                   ← Admin: quota management
services/storage/encryption.mdx               ← Admin: encryption type create
services/storage/migration.mdx                ← Admin: volume migration
services/storage/thin-provisioning.mdx        ← Admin: backend config
services/storage/backup-backends.mdx          ← Admin: backup config
services/storage/backup-config.mdx            ← Admin: backup settings
services/storage/external-storage.mdx         ← Admin: external backends
services/storage/security.mdx                 ← Admin: storage security
```

### P1-C: Networking (12 pages) — PRIORITY 3
**Skyline menu**: Network > Networks, Routers, Floating IPs, Ports, Security Groups, QoS Policies, VPNs, Firewalls, Topology
**Skyline code**: `src/pages/network/containers/Network/`, `Router/`, `FloatingIp/`, `Port/`, `SecurityGroup/`, `QoSPolicy/`, `VPN/`, `Firewall/`, `Topology/`

Pages to rewrite:
```
services/networking/create-network.mdx        ← Network create form
services/networking/subnets.mdx               ← Subnet create (within network detail)
services/networking/routers.mdx               ← Router create + interface management
services/networking/floating-ips.mdx          ← Allocate + associate floating IP
services/networking/security-groups.mdx       ← Security group + rules create
services/networking/dns-config.mdx            ← DNS config in network/subnet
services/networking/vpn.mdx                   ← VPN (IKE, IPsec, site connections)
services/networking/qos.mdx                   ← Admin: QoS policy create
services/networking/quotas.mdx                ← Admin: network quotas
services/networking/dhcp.mdx                  ← Admin: DHCP agent management
services/networking/ipam.mdx                  ← Admin: IP management
services/networking/network-agents.mdx        ← Admin: network agents list
```

### P1-D: Load Balancer (5 pages) — PRIORITY 4
**Skyline menu**: Network > Load Balancers (multi-step create wizard)
**Skyline code**: `src/pages/network/containers/LoadBalancers/`
**Endpoint**: octavia

Pages to rewrite:
```
services/load-balancer/create-lb.mdx          ← LB Create wizard (multi-step)  [NOTE: check if this file exists, may be different name]
services/load-balancer/listeners.mdx          ← Listener create
services/load-balancer/pools.mdx              ← Pool create
services/load-balancer/health-monitors.mdx    ← Health monitor create
services/load-balancer/floating-ip.mdx        ← Floating IP for LB
services/load-balancer/lb-quotas.mdx          ← Admin: LB quotas
```

### P1-E: Images (8 pages) — PRIORITY 5
**Skyline menu**: Compute > Images (user + admin)
**Skyline code**: `src/pages/compute/containers/Image/`

Pages to rewrite:
```
services/images/upload-image.mdx              ← Image create/upload form
services/images/create-snapshot.mdx           ← Snapshot (from Instance page)
services/images/get-images.mdx                ← Image list columns
services/images/share-images.mdx              ← Image share/accept
services/images/image-properties.mdx          ← Image metadata edit
services/images/image-templates.mdx           ← Admin: image management
services/images/metadata.mdx                  ← Admin: metadata definitions
services/images/quotas.mdx                    ← Admin: image quotas
```

### P1-F: Object Storage (5 pages) — PRIORITY 6
**Skyline menu**: Storage > Object Storage
**Skyline code**: `src/pages/storage/containers/Container/`
**Endpoint**: swift

Pages to rewrite:
```
services/object-storage/create-container.mdx  ← Container create
services/object-storage/upload-objects.mdx    ← Object upload
services/object-storage/access-control.mdx    ← Container ACL
services/object-storage/versioning.mdx        ← Container versioning
services/object-storage/storage-policies.mdx  ← Admin: policies
```

### P1-G: Orchestration (4 pages) — PRIORITY 7
**Skyline menu**: Orchestration > Stacks
**Skyline code**: `src/pages/heat/containers/Stack/`
**Endpoint**: heat

Pages to rewrite:
```
services/orchestration/getting-started.mdx    ← Stack create form
services/orchestration/stacks.mdx             ← Stack management
services/orchestration/autoscaling.mdx        ← Autoscaling stacks
services/orchestration/configuration.mdx      ← Admin: Heat config
```

---

## Phase 2: Admin-Only Services (25 pages)

These services appear ONLY in the Skyline admin menu. Docs in user-guide/ sections need admin-scope callouts.

### P2-A: Identity (7 pages)
**Skyline menu (admin)**: Identity > Domains, Projects, Users, User Groups, Roles, RBAC Management
**Skyline menu (user)**: Identity > Projects, Users, User Groups, Roles (limited)
**Skyline code**: `src/pages/identity/containers/`

Pages to rewrite:
```
services/identity/projects.mdx                ← Project create/edit
services/identity/users.mdx                   ← User create/edit
services/identity/roles.mdx                   ← Role assignment
services/identity/domain-management.mdx       ← Admin: Domain management
services/identity/application-credentials.mdx ← User: App credentials
services/identity/multi-factor-auth.mdx       ← User: MFA setup
services/identity/service-catalog.mdx         ← Admin: Service catalog
```

### P2-B: Resource Optimizer / Watcher (8 pages)
**Skyline menu (admin-only)**: Optimization > Goals, Strategies, Audit Templates, Audits, Action Plans, Actions
**Skyline code**: `src/pages/watcher/containers/`
**Endpoint**: watcher

Pages to rewrite:
```
services/optimization/user-guide/run-audit.mdx        ← Audit create
services/optimization/user-guide/action-plans.mdx      ← Action plan list/detail
services/optimization/user-guide/execute-actions.mdx    ← Execute action plan
services/optimization/user-guide/audit-history.mdx      ← Audit history list
services/optimization/admin-guide/scheduling.mdx        ← Audit template create
services/optimization/admin-guide/action-policies.mdx   ← Action policies
services/optimization/admin-guide/compute-integration.mdx ← Compute integration
services/optimization/admin-guide/security.mdx          ← Security config
```

### P2-C: Monitoring (10 pages)
**Skyline menu (admin-only)**: Monitor Center > Overview, Physical Nodes, Storage Clusters, OpenStack Services, Other Services, Monitoring, Logging, Activity Log, Cluster Health
**Skyline code**: `src/pages/monitor/containers/`

Pages to rewrite:
```
services/monitoring/user-guide/dashboards.mdx           ← Monitor Overview
services/monitoring/user-guide/metrics-alerts.mdx       ← Monitoring page
services/monitoring/user-guide/log-analytics.mdx        ← Logging page
services/monitoring/user-guide/network-monitoring.mdx   ← Network monitoring
services/monitoring/user-guide/alert-rules.mdx          ← Alert rules
services/monitoring/admin-guide/alert-channels.mdx      ← Alert channels
services/monitoring/admin-guide/ddos-protection.mdx     ← DDoS protection
services/monitoring/admin-guide/log-collection.mdx      ← Log collection
services/monitoring/admin-guide/metric-endpoints.mdx    ← Metric endpoints
services/monitoring/admin-guide/retention.mdx           ← Data retention
```

---

## Phase 3: Special Services (24 pages)

### P3-A: Kubernetes / K8SaaS (11 pages)
**Skyline menu**: Container > Clusters, Cluster Templates (user + admin)
**Skyline code**: `src/pages/container-infra/containers/`
**Endpoint**: magnum

### P3-B: Disaster Recovery (9 pages) — DO NOT REWRITE GUI
**XDR is Dashboard-only (Hystax UI), NOT Skyline.** Keep existing Dashboard descriptions as-is.
Only fix: branding (no "Hystax"), nav path corrections if needed.

### P3-C: SDS (4 pages) — DO NOT REWRITE GUI
**SDS management is via the deployment console Software Defined Storage module, NOT Skyline.** Keep existing descriptions.
Only fix: ensure the deployment console tab first in admin pages.

---

## Execution Workflow (per service)

```
1. EXPLORE: Launch Explore agent to read ALL Skyline code for the service
   - Every Create/Update/Delete JSX
   - actions/index.jsx (action wiring)
   - List index.jsx (columns, filters)
   - Detail pages (tabs, fields)
   - Menu entry (user vs admin, exact label)

2. READ DOCS: Read all existing doc pages for the service

3. REWRITE: Update each page with exact Skyline form fields
   - Dashboard tabs: exact field names, types, options from code
   - Nav paths: match Skyline sidebar labels exactly
   - Admin-only features: add Warning callout
   - CLI tabs: keep/improve existing CLI commands

4. VERIFY: Run local Mintlify dev server, check HTTP 200 on all pages

5. REVIEW: Run /review-docs <service> (3-agent pipeline)
   - GUI accuracy agent
   - Branding & tone agent  
   - Structure & links agent

6. FIX: Address any review issues

7. MARK DONE: Update this plan
```

---

## Metrics

| Metric | Count |
|--------|-------|
| Total pages with Dashboard tabs | 137 |
| Already done | 13 |
| Remaining to rewrite | 119 |
| Phase 1 (core user services) | 69 |
| Phase 2 (admin-only services) | 25 |
| Phase 3 (special services) | 25 (11 rewrite + 14 light-touch) |
| DO NOT TOUCH (XDR + SDS) | 13 |

---

## Rules

1. **Always read Skyline code FIRST** — never guess form fields from Horizon knowledge
2. **Cross-validate every field** — name, label, type, required, disabled, options, defaults, validation
3. **Check admin vs user scope** — admin-only features need Warning callout
4. **Match menu labels exactly** — including hyphens, casing
5. **No "Horizon", "Masakari", "Designate" etc. in prose** — full branding compliance
6. **No icon in frontmatter** on user/admin guide sub-pages
7. **Dashboard tab first** in user guides, the deployment console tab first in admin guides
8. **Never commit without asking** — make edits, wait for explicit push instruction
