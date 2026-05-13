# Xloud Documentation — Complete Knowledge Dump

**Generated**: 2026-03-31
**Source**: Memory files, CLAUDE.md, authoring guidelines, rules files, and full conversation history

---

## 1. PROJECT OVERVIEW

- **Repo**: `/home/ankur/Ankur-Workspace/docs/`
- **Platform**: Mintlify (docs-as-code, MDX format)
- **Config**: `docs.json` — navigation, theme, fonts, footer
- **URL**: https://docs.xloud.tech
- **Branch**: `main` = production, `staging` = working
- **Total pages**: ~250+ MDX files across 15+ service sections
- **Guidelines**: `.claude/doc-authoring-guidelines.mdx` (471 lines, MUST read before writing)

---

## 2. CRITICAL RULES (NON-NEGOTIABLE)

1. **No emojis anywhere** — not in MDX content, descriptions, tables, docs.json, or any file
2. **Never commit or push without explicit instruction** — make file edits only, wait for "commit" or "push"
3. **Never create pages with invented content** — only write from provided sources, links, screenshots, or explicit instructions
4. **Always invoke `/mintlify` skill** before creating or editing any page
5. **Always read `.claude/doc-authoring-guidelines.mdx`** before writing
6. **XDeploy-first for admin guides** — show XDeploy UI steps as primary method, CLI as secondary in Accordion/Tab

---

## 3. BRANDING & TERMINOLOGY

### Customer-Facing Names (from public content guardrails)

| Internal Name | Customer-Facing Name |
|---|---|
| Watcher | Resource Optimizer / Dynamic Cluster Optimization |
| FileFS | File-Level Restore |
| xDeploy | Deployment Wizard / Management Platform |
| XAVS-Ansible | Deployment Automation |
| Nova xloud-adjust | Live Resource Scaling |
| Wazuh | Integrated Security Platform |
| Ceph | Distributed Storage / XSDS |
| OVN/Neutron | Software-Defined Networking |
| KVM/QEMU/libvirt | Native Hypervisor (KVM naming OK in tech context) |
| OpenStack | Xloud (in prose) / OpenStack (in CLI commands only) |
| Kolla-Ansible | XAVS Deployment Automation |
| Hystax Acura | XDR (never mention Hystax) |

### Service Mapping

| OpenStack Service | Xloud Name | Notes |
|---|---|---|
| Nova | Xloud Compute | |
| Cinder | Xloud Block Storage | |
| Neutron | Xloud Networking | |
| Glance | Xloud Image Service | |
| Keystone | Xloud Identity | |
| Swift | Xloud Object Storage | |
| Octavia | Xloud Load Balancer | |
| Barbican | Xloud Key Management / KMS | |
| Designate | Xloud DNS | |
| Manila | Xloud Shared Filesystem | |
| Masakari | Xloud High Availability / Instance HA | |
| Heat | Xloud Orchestration | |
| Horizon | Xloud Dashboard (current) → XCONNECT (future) | |

### Where "OpenStack" IS acceptable
- CLI commands: `openstack server list`, `python-openstackclient`
- Config keys: `openstack_sd_configs`
- Package names: `python3-openstackclient`
- Terraform provider: `hashicorp/openstack`
- HTTP headers: `X-OpenStack-Nova-Microversion`
- Horizon UI button: "Download OpenStack RC File"

### Where "OpenStack" is NOT acceptable
- Prose descriptions: "OpenStack API layer" → "Xloud API layer"
- Prerequisites: "OpenStack CLI configured" → "Xloud CLI configured"
- Marketing text: never say "OpenStack cloud" → "Xloud platform"

### Tech names that ARE OK to use
- KVM, OVN, OVS, Ceph, HAProxy, RabbitMQ, MariaDB, Prometheus, Grafana, OpenSearch
- Internal service names: Nova, Cinder, Neutron, Glance, Keystone, Heat, Octavia, Barbican, Designate, Masakari, Watcher, Manila, Swift, Ironic, Magnum

### Names that are NOT OK in prose
- "OpenStack" — always use "Xloud" in prose (OK only inside CLI commands, config keys, package names, Terraform provider)

### NEVER reveal publicly
- Repo counts, commit counts, LOC, tech stack specifics, team size, cluster topology, compliance matrix structure, internal service connections

---

## 4. COMPANY & PRODUCTS

### Company Info
- **Name**: Xloud Technologies Private Limited
- **Address**: A 307, Ansal Chamber 1, Bhikaji Cama Place, Delhi 110066
- **Email**: info@xloud.tech, support@xloud.tech
- **Phone**: +91-9289062555
- **Tagline**: "Helping India build their Next-Gen Cloud Infra"
- **Colors**: Primary `#197560`, Light `#3F8F7E`, Dark `#145C4C`
- **Fonts**: Gilroy (headings), Tenorite (body)

### Products
| Product | Full Name | Description |
|---|---|---|
| XAVS | Advanced Virtualization Suite | VM and container management |
| XPCI | Private Cloud Infrastructure | Full cloud platform |
| XHCI | Hyper Converged Infrastructure | Compute+storage+networking consolidated |
| XSDS | Software Defined Storage | Ceph-based block, object, file |
| XIMP | Infrastructure Monitoring Platform | Prometheus+Grafana+OpenSearch+Wazuh |
| XDR | Disaster Recovery | Hystax-based, Dashboard-only (no CLI) |
| XNAS | NAS Storage | SMB, NFS, AFP, FTP, snapshots, HA |
| XNexus | Unified Storage | Dell HW, coming soon |
| XOS | Operating System | Custom Ubuntu 24.04 |
| XMS | Migration Suite | 10+ platforms, AI scoring (separate product from XIMP) |
| xInsight-AI | AI-Powered Ops | 42 MCP tools, on-premises LLM (separate product from XNexus) |

### Product Page Rules
- XSDS is the example — keep all product pages minimal like XSDS
- Max 4 services per product page
- Link to website for full details: `https://xloud.tech/contact`
- Each product page links to docs pages, not website pages
- XMS is SEPARATE from XIMP
- xInsight-AI is SEPARATE from XNexus

---

## 5. XDEPLOY (DEPLOYMENT MODULE)

### What it is
- Cockpit-based web UI on deployment node
- 12 modules in the sidebar
- NOT installed on all nodes — only deployment node

### Module Structure (from actual code)

| Module | Tabs | Config Path |
|---|---|---|
| Bootstrap | Overview, Hardware, Dependencies, Logs | System detection |
| Hosts | Hosts, SSH Access, DNS, Logs | `/etc/xavs/nodes` |
| Configuration | Basics, Network, Storage, Load Balancer, Monitoring, Advance Features, Custom Config, Logs | `/etc/xavs/globals.d/_99_xavs.yml` |
| Advanced Config | 3-panel: Service Tree + Code Editor + File Browser | `/etc/xavs/config/{service}/` |
| Images | Overview, Extract/Pull, Registry, Logs | Docker images |
| Operations | Deploy, Manage, Backend, Advanced (23 total commands) | Runs xavs-ansible |
| Management | User Management, Scaling | OpenStack users/workers |
| Cloud Fleet | Topology map, host list, connections | Cluster visualization |
| XSDS | Bootstrap Config, Storage Tiers, Config File, Logs | Ceph management |
| Cluster License | License dashboard, activation | `.xlic` files |
| XDeploy Key | Activation status, key management | Hardware-bound key |

### Configuration Tab Field Names (from code)

**Advance Features toggles:**
```
enable_kms                           → enables barbican
enable_host_ha                       → enables masakari + hacluster
enable_dynamic_cluster_optimization  → enables watcher
enable_db_backup_utility
enable_proxysql
enable_disk_encryption               → enables barbican + encryption flags
docker_insecure_registry
```

**Storage backends available:**
LVM, Ceph RBD, NFS, iSCSI, VMware VMDK, VMware vStorage, Hitachi NAS, Quobyte, Pure Storage (iSCSI/FC/NVMe-RoCE)

**Monitoring toggles:**
```
enable_prometheus, enable_grafana, enable_central_logging, enable_prometheus_alerts
```
When alerts enabled: SMTP server, from/to emails, SMTP password, webhook URL, Test buttons

### Advanced Configuration Service Paths
All services at `/etc/xavs/config/{service}/`:
nova, glance, keystone, neutron, cinder, placement, horizon, heat, ironic, octavia, magnum, mistral, masakari, barbican, manila, designate, watcher, ceilometer, gnocchi, prometheus, grafana, opensearch, fluentd, haproxy, redis + 10 more

### XDeploy Steps Pattern (for admin guide pages)
```
1. Open XDeploy → Configuration
2. Go to relevant tab (e.g., Advance Features)
3. Toggle setting to Yes / configure fields
4. Click Save Configuration
5. Go to Operations → run deploy/reconfigure
```

For config file edits:
```
1. Open XDeploy → Advanced Configuration
2. Select service in Service Tree (left panel)
3. Create/select config file in File Browser (right panel)
4. Edit in Code Editor (center panel)
5. Click Save Current File
6. Go to Operations → run reconfigure
```

---

## 6. XLOUD-DEVELOPED FEATURES (82 total, 51% undocumented)

### P0 — Competitive Differentiators
1. **Agentless File-Level Restore** (FileFS) — browse snapshot filesystems, download individual files
2. **Bidirectional CPU Hotplug** — add AND remove vCPUs (competitors only add)
3. **3 Memory Methods** — balloon + DIMM + virtio-mem unique combination
4. **Combined Manual+Auto Storage Tiering** — user picks tier + optimizer auto-moves
5. **Built-in SIEM** (Security Posture Panel) — 8-tab Wazuh dashboard
6. **XMS Migration Suite** — 10+ source platforms, AI scoring
7. **xInsight-AI** — on-premises NLP cloud management, 42 MCP tools
8. **Per-Volume Selective Encryption** — encrypt individual volumes
9. **Triple Compliance Scanning** — SCA + Lynis + OpenSCAP

### Key Feature Areas
- **Compute**: Live vCPU/RAM, NUMA, CPU pinning, hugepages, EVC, vTPM, live migration, server groups, atomic upgrades, horizontal scaling, app-consistent snapshots, multi-hypervisor, bare metal, heterogeneous hardware
- **Resource Optimization**: DRS workload balancing, storage tier auto-balance, server group awareness, 14 strategies
- **Dashboard**: Security posture panel, cluster health dashboard, global notification bell, global search (22 types), right-click context menu, snapshot file browser, volume live retype, monitoring panels, HA status panel
- **Security**: Wazuh SIEM, OS hardening (CIS), OpenSCAP, Lynis, Grafana security ops dashboard, self-healing credentials, active response, cert expiry monitoring, custom detection rules, AlertManager rules, SBOM CI pipeline
- **Self-Healing**: VM HA (Masakari), power recovery (9-phase), container autoheal (3-tier), 120 alert rules, network resilience (VRRP), rolling upgrades with rollback

### Mark Xloud-developed features with:
```mdx
<Info>**Xloud-Developed** — This capability is developed by Xloud and ships with XAVS / XPCI.</Info>
```

---

## 7. DISASTER RECOVERY

- Tool: Hystax Acura (NEVER mention "Hystax" — brand as "XDR")
- **Dashboard-only** — there is NO CLI for DR operations
- CLI Reference page states: "All DR operations are managed through the XDR Dashboard"
- Capabilities: protection plans, continuous replication, one-click failover, failback, test failover, RPO/RTO monitoring, runbook automation

---

## 8. PAGE STRUCTURE (MANDATORY)

Every page follows:
```
Frontmatter (title, description, icon, sidebarTitle)
→ Overview (1 paragraph)
→ Prerequisites (<Note>)
→ Architecture/Concepts (if applicable, Mermaid diagrams)
→ Configuration/Procedure (<Tabs> with Dashboard + CLI)
→ Validation (<Check>)
→ Troubleshooting (<AccordionGroup>)
→ Next Steps (<CardGroup>)
```

### Component Minimums
- 5+ MDX components per page
- Steps for ALL sequential procedures (never plain numbered lists)
- Tabs for Dashboard/CLI (or XDeploy/CLI for admin pages)
- CodeGroup for multi-tool commands
- Callouts (Note/Warning/Tip/Danger) for important info
- Cards for navigation
- Mermaid for architecture

### Prohibited Patterns
- Plain markdown where MDX component exists
- Inline "Note:" text (use `<Note>` callout)
- Bare numbered lists for procedures (use `<Steps>`)
- Walls of text (break into Accordions/Tabs/Cards)
- Emojis (ABSOLUTE ban)

---

## 9. ICONS

Mintlify uses **Lucide** icons. Common valid names:
```
server, shield, cpu, hard-drive, network, search, settings,
alert-triangle, check, info, lock, key, globe, database,
monitor, layers, power, terminal, code, wrench, play,
arrow-right, arrow-left-right, shield-check, sliders, activity
```

Known INVALID icons (replaced in past sessions):
```
triangle-exclamation → alert-triangle
shield-halved → shield-check
arrows-left-right → arrow-left-right
network-wired → network
memory → hard-drive or cpu
gear → settings
circuit-board → cpu
layer-group → layers
power-off → power
bar-chart-2 → chart-bar
```

---

## 10. NAVIGATION STRUCTURE (docs.json)

### Top-Level Groups
1. Getting Started (introduction, cli-setup, deployment/index)
2. Products (11 product pages)
3. Core Services (Compute, Block Storage, Networking, Images, Orchestration, Identity, Dashboard)
4. Other Services (Load Balancer, DNS, Key Manager, Object Storage, SDS, Monitoring, DR, Instance HA, K8s, Resource Optimizer)
5. Security (infrastructure, VM, API, data, network, compliance, hardening, wazuh, lynis, openscap)
6. Deployment (12 XDeploy pages)
7. Integrations (terraform, ansible, prometheus, grafana, wazuh)

### Per-Service Pattern
```
services/<service>/
  index.mdx          # Service overview
  user-guide.mdx     # User guide index (with sub-pages)
  admin-guide.mdx    # Admin guide index (with sub-pages)
  cli-reference.mdx  # CLI reference (plain page, NOT dropdown group)
```

---

## 11. USER GUIDE RULES

- Written for **non-technical end users**
- Dashboard tab FIRST, CLI tab second
- Use `source openrc.sh` (NOT `admin-openrc.sh`) — users don't have admin credentials
- No `systemctl`, `docker exec`, kernel commands, or admin-level operations
- Replace jargon: Glance→platform image, Cinder→block storage volume, tenant→project, OSD→storage device
- Where admin action needed: "Your administrator can configure this through [XDeploy](/deployment)"
- Resource Optimizer and Monitoring dashboards require admin role — add `<Warning>` callout

### Custom CLI tools
- `watcher` — Resource Optimizer CLI (prefix with `openstack`: `openstack watcher audit create`)
- `ximp` — XIMP monitoring CLI (available on management node only)
- `xdr` — DOES NOT EXIST (DR is Dashboard-only)

---

## 12. ADMIN GUIDE RULES

- Written for **technical administrators**
- XDeploy tab FIRST, CLI tab second
- Show exact XDeploy UI flow with Steps
- Manual config editing goes in CLI tab as secondary method
- Service credentials and database connections are AUTO-MANAGED by XDeploy — note this clearly
- Always end config changes with: "Go to Operations → run reconfigure"
- Reference correct paths: `/etc/xavs/config/{service}/` for Advanced Configuration

### XDeploy Tips already added to these admin pages:
storage/admin-guide, networking/admin-guide, load-balancer/admin-guide, monitoring/architecture, key-manager/admin-guide, instance-ha/admin-guide, optimization/admin-guide, storage/encryption, sds/architecture, sds/storage-tiers, monitoring/alert-channels, security/wazuh

---

## 13. DEPLOYMENT DOCS

### Pre-deployment checklist order:
1. XOS running on all nodes
2. Plan network (API/MGMT, VM traffic, LB, Storage, Replication VLANs)
3. Prepare DNS and domain names + SSL
4. Gather credentials (SSH from deployment node, license from license.xloud.tech)
5. Architecture decision (AIO / HCI / Distributed)

### Deployment workflow order:
XDeploy Key → Bootstrap → Hosts → XSDS (if using) → Configuration → Images → Operations → Management → Cloud Fleet → Cluster License

---

## 14. FILE PATHS

| Context | Path Pattern |
|---|---|
| Service config (XDeploy Advanced Config) | `/etc/xavs/config/{service}/{filename}` |
| Global config | `/etc/xavs/globals.d/_99_xavs.yml` |
| Passwords | `/etc/xavs/passwords.yml` |
| Inventory | `/etc/xavs/nodes` |
| Container logs | `/var/log/kolla/{service}/` (keep as-is) |
| Container config files | `/var/lib/kolla/config_files/` (keep as-is) |
| Certificates | `/etc/xavs/certificates/` |
| YAML config keys | `kolla_enable_tls_*` (keep as-is — actual config keys) |

---

## 15. AUDIT RESULTS (2026-03-31)

### CEO Audit Score: 7.5/10

**Strengths**: Deployment section production-ready, consistent enterprise template, honest product pages, comprehensive security section, well-organized navigation

**Fixed Issues**:
- Invented `xdr` CLI removed (DR is Dashboard-only)
- "OpenStack" replaced with "Xloud" in prose (11 files)
- Duplicate chmod in hardening guide removed
- Kolla → XAVS in prose (12 files, /var/log/kolla and /var/lib/kolla kept)
- admin-openrc.sh → openrc.sh in 20 user guide files
- XDeploy-first Tabs in 23 admin guide pages
- 86+ icon replacements for valid Lucide names
- 12 broken links fixed
- OpenStack jargon replaced in user guides

**Remaining gaps**: 42 of 82 features undocumented (51%), "Coming soon" on homepage for XNexus, XCONNECT roadmap exposed on dashboard page

---

## 16. COMMIT CONVENTIONS

- `docs:` for content changes
- `config:` for docs.json/meta changes
- `fix:` for bug fixes (broken links, icons, parse errors)
- Always end with: `Co-Authored-By: Claude Opus 4.6 (1M context) <noreply@anthropic.com>`
- Use HEREDOC for commit messages

---
