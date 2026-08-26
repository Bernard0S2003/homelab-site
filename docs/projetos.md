# 🚀 Projects & DevOps Practices

Overview of operational engineering processes, change-control regimes, and active project planning.

---

## ⚙️ CI/CD & Infrastructure as Code (GitOps)

To prevent configuration drift and promote clean orchestration, system state is maintained declaratively:

*   **Centralized Version Control:** All Docker Compose assets, proxy configurations, and Proxmox or OPNsense layout states are versioned inside private repositories on the local **Forgejo** instance.
*   **Change-control Workflows:** Upgrades, configurations alterations, or new container additions are deployed declaratively. This ensures that the environment is fully rebuildable (Disaster Recovery model) within minutes directly from source control assets.

---

## 🛡️ Backup & High Availability Policies

*   **Kopia Backup Engine:** Provides client-side encryption, deduplication, and compression of persistent docker volume states. Backups execute on cron schedules, pushing snapshots to isolated local targets and secondary remote cloud vaults.
*   **Block-Level Snapshots (Proxmox PBS):** Automated system-level backups of active LXC hosts and standalone VMs, enabling minimal downtime restorations.

---

## 🔮 Operational Roadmap

### Core Automation & IaC
- [x] Domain consolidation and wildcard DNS-01 certificate challenges on Traefik proxy.
- [x] Combined telemetry alerts sent directly to dedicated Discord notification threads.
- [ ] Orchestration of container creation and configurations using Ansible playbooks.
- [ ] Transitioning container host endpoints management into GitOps-controlled Portainer instances.

### Security & Hardening
- [x] SSO authentication gateways established via Authentik OIDC providers with enforced Multi-Factor Authentication (MFA).
- [ ] Implementing a staging cluster configuration using Proxmox Linked Clones to run automated code validations (Test-driven infrastructure updates).
