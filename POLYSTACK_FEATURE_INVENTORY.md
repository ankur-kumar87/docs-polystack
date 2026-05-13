# Polystack Complete Feature Inventory vs Documentation Coverage

**Generated**: 2026-03-20
**Sources**: POLYSTACK_BIBLE (37 features), DEVELOPMENT-TRACKER, 26 compliance docs, 35 blueprints, 7 selfheal guides, comparison matrices (430+ features), 30 verified LinkedIn posts, all rules files
**Total Repos**: 24 | **Total Commits**: 11,000+ | **Compliance Points**: 76

---

## CRITICAL: PUBLIC CONTENT GUARDRAILS

Documentation MUST use customer-facing names (from `polystack-public-content-guardrails.md`):

| Internal Name | Customer-Facing Name |
|---|---|
| Watcher | Automated Workload Optimization / Resource Optimizer |
| FileFS | File-Level Restore |
| Deployment Console | Deployment Wizard / Management Platform |
| Ironcore-Ansible | Deployment Automation |
| Nova polystack-adjust | Live Resource Scaling |
| Wazuh | Integrated Security Platform |
| Ceph | Distributed Storage |
| OVN/Neutron | Software-Defined Networking |
| KVM/QEMU/libvirt | Native Hypervisor |
| OpenStack | Polystack Platform (or just avoid mentioning) |

**NEVER reveal**: repo count, commit count, LOC, tech stack specifics, team size, cluster topology, compliance matrix structure, internal service connections.

---

## LEGEND

| Status | Meaning |
|--------|---------|
| DOCUMENTED | Has a dedicated page or substantial section |
| PARTIAL | Mentioned briefly, needs expansion |
| MISSING | No documentation exists |
| N/A-DOCS | Backend/infra only, no user-facing docs needed |

---

## CATEGORY A: COMPUTE (Nova — 10 commits over upstream)

| # | Feature | CP | Doc Status | Current Page | Gap |
|---|---------|-----|-----------|--------------|-----|
| A1 | **Live vCPU/RAM Scaling** | CP-002 | DOCUMENTED | `compute/live-resize.mdx` | Good. Needs bidirectional differentiator callout |
| A2 | Bidirectional CPU (add+remove) | CP-002 | PARTIAL | mentioned in live-resize | Not called out as unique vs VMware/Nutanix (add-only) |
| A3 | 3 Memory Methods (balloon+DIMM+virtio-mem) | CP-002 | PARTIAL | troubleshooting only | Each method needs explanation |
| A4 | CPU Topology Awareness (SMT/threads) | CP-002 | MISSING | — | Thread alignment, 5-method SMT detection |
| A5 | PCI Device Hotplug | — | MISSING | — | Controller exists, undocumented |
| A6 | **NUMA-Aware Scheduling** | CP-003 | PARTIAL | `compute/advanced-features.mdx` | Needs full page: NUMA cells, pinning, hugepages |
| A7 | **CPU Pinning** (dedicated/shared/mixed) | CP-003 | PARTIAL | mentioned in advanced-features | Needs dedicated section |
| A8 | **Hugepages** (2MB/1GB) | CP-003 | PARTIAL | mentioned | Needs section |
| A9 | **CPU Feature Masking (EVC equivalent)** | CP-003 | MISSING | — | Per-flavor granularity vs VMware cluster-wide |
| A10 | **vTPM 2.0** | CP-004 | PARTIAL | accordion in advanced-features | Needs full page: Barbican secret, live migration |
| A11 | **Live Migration** | CP-009 | DOCUMENTED | `compute/live-migration.mdx` | Needs Polystack enhancements (cross-CPU, vTPM, automated) |
| A12 | **Server Groups** (affinity/anti-affinity) | CP-007 | DOCUMENTED | `compute/server-groups.mdx` | Needs Watcher enforcement callout |
| A13 | **Atomic Container Upgrades** | CP-005 | MISSING | — | Per-service rollback in 2-10s |
| A14 | **Horizontal Scaling** (no node cap) | CP-006 | MISSING | — | No hard limit, Cells v2, proven at CERN 8K+ nodes |
| A15 | **App-Consistent Snapshots** (quiesce) | CP-001 | PARTIAL | warning in create-snapshot | Needs full section: guest agent, fsfreeze, VSS |
| A16 | **Multi-Hypervisor** (KVM+VMware) | CP-010 | MISSING | — | Single console for both hypervisors |
| A17 | **Bare Metal Provisioning** (Ironic) | CP-011 | PARTIAL | `compute/bare-metal.mdx` | Check if it covers PXE/IPMI/Redfish detail |
| A18 | **Heterogeneous Hardware** | CP-012 | MISSING | — | Mixed nodes, CPUs, media in one cluster |

## CATEGORY B: RESOURCE OPTIMIZATION (Watcher — 12 commits over upstream)

| # | Feature | CP | Doc Status | Current Page | Gap |
|---|---------|-----|-----------|--------------|-----|
| B1 | **DRS Workload Balancing** | CP-008 | PARTIAL | `optimization/admin-guide/strategy-config.mdx` | Polystack enhancements (safety checks, max_iterations) not called out |
| B2 | **Storage Tier Auto-Balance** | F-025 | PARTIAL | `storage/storage-tiers.mdx` | Watcher auto-tiering strategy not mentioned |
| B3 | **Server Group Awareness** | CP-007 | MISSING | — | All 14 strategies respect affinity constraints |
| B4 | **14 Strategies Total** | — | PARTIAL | strategy-config page lists them | Polystack production enhancements not highlighted |

## CATEGORY C: DASHBOARD (Horizon — 94 commits over upstream)

| # | Feature | CP | Doc Status | Current Page | Gap |
|---|---------|-----|-----------|--------------|-----|
| C1 | **Security Posture Panel** (8-tab Wazuh) | CP-045 | MISSING | — | 8 tabs, 1,847-line API, 31 commits |
| C2 | **Cluster Health Dashboard** (5-tab) | — | MISSING | — | Ceph, OpenStack, RabbitMQ, MariaDB, Alerts |
| C3 | **Global Notification Bell** | — | MISSING | — | Multi-source alerts, audio beep, browser notifications |
| C4 | **Global Search** (22 resource types) | CP-061 | PARTIAL | `dashboard/user-guide.mdx` | Needs dedicated usage page |
| C5 | **Right-Click Context Menu** | F-031b | PARTIAL | mentioned briefly | Needs usage guide |
| C6 | **Snapshot File Browser** (FileFS) | — | MISSING | — | Agentless file restore — major differentiator |
| C7 | **vTPM UI** (Flavor+Image+Instance) | CP-004 | PARTIAL | accordion | Needs full page |
| C8 | **Volume Live Retype** | F-022 | MISSING | — | Admin storage migration |
| C9 | **Monitoring & Logging Panels** | F-021 | PARTIAL | monitoring/ section | Embedded Grafana/OpenSearch not documented |
| C10 | **HA Status Panel** (Masakari) | — | MISSING | — | Segments, hosts, notifications, evacuation |
| C11 | **Dark Mode** | F-031 | N/A-DOCS | — | Auto-detected from system preference |
| C12 | **License Enforcement** | CP-002 | N/A-DOCS | — | Backend middleware |

## CATEGORY D: SECURITY & COMPLIANCE (ironcore-ansible — 154 commits)

| # | Feature | CP | Doc Status | Current Page | Gap |
|---|---------|-----|-----------|--------------|-----|
| D1 | **Wazuh SIEM Full Stack** | CP-045 | PARTIAL | `security/wazuh.mdx` | 95 commits of detail not covered |
| D2 | **OS Hardening (CIS Benchmark)** | — | PARTIAL | `security/hardening-guide.mdx` | Polystack-specific roles not covered |
| D3 | **OpenSCAP Compliance** | — | PARTIAL | `security/openscap.mdx` | May need Polystack config detail |
| D4 | **Lynis Audit** | — | PARTIAL | `security/lynis.mdx` | May need Polystack config detail |
| D5 | **Grafana Security Ops Dashboard** | — | MISSING | — | Auto-deployed with Wazuh panels |
| D6 | **Self-Healing Credentials** (3-layer) | ENH-11 | MISSING | — | Post-deploy + cron + filesystem guardian |
| D7 | **Wazuh Master Failover** | CR-02 | MISSING | — | Manual failover playbook |
| D8 | **AlertManager Rules** (12 default) | — | MISSING | — | Node, OpenStack, Ceph, infra groups |
| D9 | **Cert Expiry Monitoring** | — | MISSING | — | Prometheus metric + 2 alert rules |
| D10 | **Custom Detection Rules** (6 Docker rules) | — | MISSING | — | Rule IDs 100100-100199 |
| D11 | **Active Response** (firewall-drop, host-deny) | — | MISSING | — | SSH brute force auto-block |
| D12 | **SBOM CI Pipeline** | CP-050 | MISSING | — | Trivy+Syft+cosign supply chain security |
| D13 | **Triple Compliance** (SCA+Lynis+OpenSCAP) | CP-045 | MISSING | — | Three independent scanners |

## CATEGORY E: DEPLOYMENT & LIFECYCLE (Deployment Console + ironcore-ansible)

| # | Feature | CP | Doc Status | Current Page | Gap |
|---|---------|-----|-----------|--------------|-----|
| E1 | **Deployment Wizard** (18 modules) | — | MISSING | — | Should be major docs section |
| E2 | **Security Compliance Module** (scanning UI) | I-003 | MISSING | — | CIS comparison, Lynis scoring |
| E3 | **AlertManager Config UI** | — | MISSING | — | SMTP/Webhook configuration |
| E4 | **Ceph Storage Tiering UI** | F-004/F-005 | MISSING | — | Software-Defined-Storage tier management |
| E5 | **LCM** (22 CLI commands) | CP-072 | MISSING | — | Full lifecycle management |
| E6 | **Safe Day-2 Operations** (dry-run) | CP-074 | MISSING | — | --check, --diff, guardrails |
| E7 | **Pre-Deployment Validation** | CP-073 | MISSING | — | 50+ checks, stress testing |

## CATEGORY F: STORAGE (Cinder + Ceph)

| # | Feature | CP | Doc Status | Current Page | Gap |
|---|---------|-----|-----------|--------------|-----|
| F1 | **Storage Tiering** (NVMe/SSD/HDD) | CP-013 | PARTIAL | `storage/storage-tiers.mdx` | Needs auto-tiering, Software-Defined-Storage UI |
| F2 | **Storage QoS** (IOPS/bandwidth) | CP-030 | PARTIAL | `storage/qos.mdx` | Bronze/Silver/Gold tiers not covered |
| F3 | **Volume Encryption** (LUKS+Barbican) | CP-043 | PARTIAL | `storage/encryption.mdx` | Per-volume selective encryption unique |
| F4 | **Manila Shared Filesystems** | CP-033 | PARTIAL | product page only | Service docs exist at `services/sds/` but Manila specifically? |
| F5 | **Object Storage** (Ceph RGW S3/Swift) | CP-034 | DOCUMENTED | `services/object-storage/` | Check if S3 compatibility documented |

## CATEGORY G: NETWORKING (Neutron/OVN)

| # | Feature | CP | Doc Status | Current Page | Gap |
|---|---------|-----|-----------|--------------|-----|
| G1 | **SDN & Microsegmentation** | CP-051/052 | PARTIAL | `networking/security-groups.mdx` | FWaaS, Tap-as-a-Service, packet logging not covered |
| G2 | **LBaaS** (Octavia) | CP-053 | DOCUMENTED | `services/load-balancer/` | Full section exists |
| G3 | **DNSaaS** (Designate) | CP-053 | DOCUMENTED | `services/dns/` | Full section exists |
| G4 | **VPNaaS** | CP-053 | MISSING | — | IPsec site-to-site tunnels |
| G5 | **Network QoS** (bandwidth/DSCP) | — | PARTIAL | `networking/qos.mdx` | Check coverage |

## CATEGORY H: SELF-HEALING & HA

| # | Feature | CP | Doc Status | Current Page | Gap |
|---|---------|-----|-----------|--------------|-----|
| H1 | **VM HA** (Masakari) | CP-005 | PARTIAL | `services/instance-ha/` | Full section exists — check Polystack specifics |
| H2 | **Power Recovery** (9-phase playbook) | — | MISSING | — | 7-13min target RTO |
| H3 | **Container Autoheal** (3-tier daemon) | — | MISSING | — | Circuit breaker, dependency graph |
| H4 | **120 Alert Rules** (13 groups) | — | MISSING | — | Predictive rules with predict_linear |
| H5 | **Network Resilience** (L3 HA, DHCP HA) | — | MISSING | — | VRRP failover 1-3s |
| H6 | **Rolling Upgrades** with rollback | — | MISSING | — | Canary deployment, image tag rollback |

## CATEGORY I: PROPRIETARY PRODUCTS

| # | Feature | Repo | Doc Status | Current Page | Gap |
|---|---------|------|-----------|--------------|-----|
| I2 | **XLicense Portal** | xlicense, 110 commits | N/A-DOCS | — | Backend portal |
| I3 | **Ironcore Guest Agent** | ironcore-guest-agent, 3 commits | MISSING | — | VSS provider for Windows app-consistent snapshots |
| I4 | **Polystack OS** (custom Ubuntu 24.04) | subiquity+cubic | PARTIAL | Polystack OS product page | No install guide |
| I5 | **Magnum** (Managed K8s) | magnum, 5,624 upstream | PARTIAL | `services/kubernetes/` | Check if it covers Magnum specifics |
| I7 | **Cyborg** (GPU/Accelerator) | cyborg, 1,058 upstream | MISSING | — | 10 drivers, GPU management |
| I8 | **Magnum Cluster API** (CAPI) | magnum-cluster-api, 855 | MISSING | — | Alternative Helm driver |

## CATEGORY J: DR & BACKUP

| # | Feature | CP | Doc Status | Current Page | Gap |
|---|---------|-----|-----------|--------------|-----|
| J1 | **Ceph RBD Mirroring** (async DR) | CP-038 | PARTIAL | `disaster-recovery/` section | Check if Ceph-native DR covered |
| J2 | **Disaster Recovery Orchestration** (Hystax Acura) | CP-038-041 | MISSING | — | Blocked on license |
| J3 | **Ceph Stretch Cluster** (RPO=0) | CP-040 | MISSING | — | Metro DR, sync replication |

## CATEGORY K: IDENTITY & GOVERNANCE

| # | Feature | CP | Doc Status | Current Page | Gap |
|---|---------|-----|-----------|--------------|-----|
| K1 | **Identity Federation** (OIDC/SAML) | CP-046 | PARTIAL | `identity/federation.mdx` | Check Keycloak bundled IdP |
| K2 | **MFA/TOTP** | CP-047 | PARTIAL | `identity/multi-factor-auth.mdx` | Check coverage |
| K3 | **Telemetry/Chargeback** (CloudKitty) | CP-065 | MISSING | — | Rating engine, showback, per-service billing |

## CATEGORY L: WORKFLOW & AUTOMATION

| # | Feature | CP | Doc Status | Current Page | Gap |
|---|---------|-----|-----------|--------------|-----|
| L1 | **Heat IaC** | CP-042 | DOCUMENTED | `services/orchestration/` | Full section exists |
| L2 | **Mistral Workflows** | CP-066 | MISSING | — | Event-driven automation engine |

---

## SUMMARY

| Status | Count | % |
|--------|-------|---|
| DOCUMENTED (full page/section) | 8 | 10% |
| PARTIAL (mentioned, needs expansion) | 28 | 34% |
| MISSING (zero documentation) | 42 | 51% |
| N/A-DOCS (no user docs needed) | 4 | 5% |
| **Total Capabilities** | **82** | |

---

## PRIORITY RANKING FOR DOCUMENTATION

### P0 — Competitive Differentiators (MUST document first)
1. **Agentless File-Level Restore** (C6) — no competitor has this
2. **Bidirectional CPU Hotplug** (A2) — only platform with hot-remove in UI
3. **3 Memory Methods** (A3) — balloon+DIMM+virtio-mem unique combination
4. **Combined Manual+Auto Storage Tiering** (F1+B2) — VMware deprecated SDRS
5. **Built-in SIEM** (C1+D1) — no competitor includes SIEM in base
7. **Per-Volume Selective Encryption** (F3) — competitors are all-or-nothing
8. **Triple Compliance Scanning** (D13) — SCA+Lynis+OpenSCAP

### P1 — Major Features
10. Cluster Health Dashboard (C2)
11. DRS with server-group awareness (B1+B3)
12. HA Status Panel (C10)
13. vTPM full page (A10)
14. Deployment Wizard (E1)
15. Global Search dedicated page (C4)
16. App-Consistent Snapshots full guide (A15)
17. Horizontal Scaling / no node cap (A14)
18. Atomic Upgrades / per-service rollback (A13)
19. Self-Healing Infrastructure (H1-H6)
20. LCM / Day-2 Operations (E5+E6)
21. Ironcore Guest Agent / VSS (I4)
22. Global Notification Bell (C3)

### P2 — Supporting Features
23-42. Volume Live Retype, GPU/Cyborg, Mistral Workflows, Chargeback, VPNaaS, Bare Metal detail, Multi-Hypervisor, Pre-Deploy Validation, SBOM/CI, AlertManager UI, Security Compliance Module, Ceph Tiering UI, Context Menu usage, Dark Mode, Wazuh Failover, Power Recovery, Container Autoheal, Alert Rules detail, Network Resilience, Rolling Upgrades

---

## VERIFIED MARKET CLAIMS (safe to use in docs, sourced)

| Claim | Source |
|---|---|
| 74% of IT leaders exploring VMware alternatives | Gartner Peer Community |
| 55+ million OpenStack cores in production | 2025 OpenStack User Survey |
| VMware 800-1500% price increases in Europe | CISPE/Network World |
| $27.2B Indian datacenter market by 2032 | MarkNtel Advisors |
| 86% of CIOs plan workload repatriation | Barclays CIO Survey |

---

## COMPETITOR CORRECTIONS (do NOT repeat these false claims)

- VMware vTPM does NOT block live migration (vSphere 7+ supports it)
- Nutanix DOES have CPU/memory hot-add (since AOS 5.1/v6.5) — only hot-remove is absent
- "No competitor has file-level restore" is FALSE — correct phrasing: "agentless file-level restore"
- CERN runs ~300K cores, NOT 1M+
