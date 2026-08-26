# 🖥️ Infrastructure & Networking

A holistic view of the homelab's hardware hosting, networking architecture, and virtualization model.

---

## 🏗️ Topology & Logical Networks

Workloads run on virtualized computing resources managed by a **Proxmox VE (PVE)** hypervisor. Traffic routing, firewall rules, and network segregation are handled centrally by a virtualized **OPNsense** appliance.

*   **Virtualization:** Isolation of core workloads inside LXC containers running nested Docker engines.
*   **Virtual Switching:** The physical network interface (`vmbr0`) connects directly to the OPNsense WAN interface. A secondary bridge (`vmbr3`) operates in **VLAN-Aware (802.1Q)** mode to segregate subnets across LXC hosts.
*   **Out-of-Band Management (OOB):** Isolated in a dedicated management VLAN to secure local administrative access.

---

## 🌐 External Access & Ingress Routing

1.  **Zero-Exposure Ingress:** WAN interfaces do not expose any direct NAT rules (port forwarding). Inbound HTTPS traffic is securely routed via outbound connections established by a **Cloudflare Tunnel** daemon terminating at the internal reverse proxy.
2.  **Secure Mesh Network:** Remote administrative access and host-to-host connectivity are provided by **Netbird**, a WireGuard-based overlay mesh VPN.

---

## 🗺️ Architecture Diagram

```mermaid
flowchart TD
    classDef hardware fill:#1E1E1E,stroke:#4CAF50,stroke-width:2px,color:#fff
    classDef network fill:#003366,stroke:#66B2FF,stroke-width:2px,color:#fff
    classDef gateway fill:#8B0000,stroke:#FF6666,stroke-width:2px,color:#fff
    classDef lxc fill:#2C3E50,stroke:#AAB7B8,stroke-width:1px,color:#fff
    classDef svc fill:#145A32,stroke:#2ECC71,stroke-width:1px,color:#fff

    CloudflareEdge((Cloudflare Edge))
    NetbirdMesh((Netbird Mesh)) -. WireGuard Tunnel .-> Node2

    subgraph PROXMOX [Proxmox VE]
        NIC0[Physical NIC0]:::hardware
        
        subgraph V_SWITCH [VLAN-Aware Virtual Switch]
            VMBR0[vmbr0: WAN Bridge]:::network
            VMBR3[vmbr3: VLAN Trunked Bridge]:::network
            VMBR90[VLAN Management Subnet]:::network
        end

        OPNSENSE{OPNsense Firewall}:::gateway

        subgraph COMPUTE [LXC Hosts]
            direction LR
            Node1[LXC proxy-node]:::lxc
            Node2[LXC iam-node]:::lxc
            Node3[LXC media-node]:::lxc
            Node4[LXC services-node]:::lxc
        end

        subgraph WORKLOADS [Docker Workloads]
            S_Traefik([Traefik Proxy]):::svc
            S_Auth([Authentik]):::svc
            S_Media([Jellyfin + Stack *arr]):::svc
            S_Vault([Open-WebUI + Immich + Nextcloud + Forgejo]):::svc
            S_SRE([Loki + Grafana + Alloy]):::svc
        end

        NIC0 ==> VMBR0
        VMBR0 ==> OPNSENSE
        OPNSENSE == Trunk ==> VMBR3
        OPNSENSE -. Mgmt .-> VMBR90

        VMBR3 --- Node1
        VMBR3 --- Node2
        VMBR3 --- Node3
        VMBR3 --- Node4

        Node1 --- S_Traefik
        Node2 --- S_Auth
        Node3 --- S_Media
        Node4 --- S_Vault
        Node4 --- S_SRE
        
        CloudflareEdge == "Outbound TCP" ===> S_Traefik
        S_Traefik -. SNI / Proxy .-> S_Auth
        S_Traefik -. SNI / Proxy .-> S_Media
        S_Traefik -. SNI / Proxy .-> S_Vault
    end

    class PROXMOX hardware
```

---

## 🛠️ LXC Nodes Breakdown

*   **Proxy Node (Edge Routing):** Handles SSL/TLS termination, automated ACME Let's Encrypt DNS-01 validation challenges, and request dispatching. Runs **Traefik** and **Cloudflared**.
*   **IAM Core Node (Identity & VPN):** Centralizes user management, acts as an OIDC/SAML provider, and manages WAN connectivity. Runs **Authentik** and the **Netbird** client.
*   **Media Node (Acquisition & Streaming):** Dedicated to media management and transcoding, featuring local hardware GPU passthrough to expedite H.264/HEVC encoding. Runs **Jellyfin** and the media downloader pipeline.
*   **Private Services Node (Data & Observability):** Houses shared repositories, document clouds, localized machine learning instances, and metrics ingestion. Runs **Nextcloud**, **Immich**, **Forgejo Git**, **Open-WebUI**, and the telemetry engine (**Loki / Grafana / Alloy**).
