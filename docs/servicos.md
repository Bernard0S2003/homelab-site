# 📦 Services & Technologies

Public catalog of active workloads running in the homelab environment, categorized by functional role.

---

## 🛡️ Security, Networks & Ingress

*   **Traefik Proxy:** The primary HTTP gateway and reverse proxy. Manages automated TLS certificate issuance and renewal using DNS-01 ACME challenge mechanisms.
*   **Netbird:** A decentralized, peer-to-peer mesh VPN utilizing the WireGuard protocol. Connects administrative clients directly to resources without exposing endpoints or public ports.
*   **Cloudflared:** Initiates secure outbound HTTPS connections to Cloudflare's Edge, routing external static site traffic safely into the network.
*   **Authentik:** High-performance Identity and Access Management platform (IAM). Enforces Single Sign-On (SSO) with Multi-Factor Authentication (MFA) and provides *Forward Auth* protection templates to shield legacy HTTP backends.

---

## 📊 Telemetry, System Health & SRE

*   **Grafana & Loki:** Centralized log grouping and processing pipeline, allowing real-time querying using LogQL syntax to monitor systems and trigger warning workflows.
*   **Grafana Alloy:** Distributed daemon agents embedded on every container host, collecting, parsing, and shipping logs or system resource telemetry.
*   **Diun (Docker Image Update Notifier):** Background daemon tracking tags of active Docker containers on public Hubs, issuing webhook notifications to alert on version increments.

---

## 📁 Storage, Collaboration & Data

*   **Nextcloud:** Private self-hosted file platform, calendar, contacts, and document manager.
*   **Immich:** High-speed media server and backup target for personal photos. Employs local machine learning engines to achieve automated object classification and face indexation.
*   **Forgejo:** Lightweight private Git forge hosting localized repositories, infrastructure setups (IaC), and orchestration code.

---

## 🧠 Local Artificial Intelligence

*   **Open-WebUI:** Advanced, web-based chat environment designed for executing inferences on localized AI LLM models.
*   **Omniroute:** Aggregator proxy and dispatcher assisting in requests routing, endpoint load-balancing, and LLM fallback orchestration.

---

## 🎬 Media Infrastructure & Automation

*   **Jellyfin:** Free software entertainment server hosting personal video library directories, integrated with active hardware GPU transcoding acceleration.
*   **Automated Download Stack (*arr Suite):** Interconnected tools automating content acquisition pipelines:
    *   **Sonarr & Radarr:** Schedule-based tracking and monitoring of media series and films.
    *   **Prowlarr:** Centralized manager distributing search indexers and trackers.
    *   **Bazarr:** Automatic subtitle grabber supporting multiple languages.
    *   **Flaresolverr:** Proxy service bypassing web challenge tasks on public directories.
