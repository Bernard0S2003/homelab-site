# 🖥️ Infraestrutura & Rede

Visão holística da infraestrutura, arquitetura de rede e modelo de virtualização do homelab.

---

## 🏗️ Topologia e Redes Lógicas

O ambiente é virtualizado sobre um hypervisor **Proxmox VE (PVE)**. O encaminhamento do tráfego, as regras de firewall e a segregação de redes são geridos centralmente por uma instância virtualizada do **OPNsense**.

*   **Virtualização:** Segregação de workloads em contentores LXC rodando instâncias de Docker integradas.
*   **Comutação Virtual:** A ponte física (`vmbr0`) liga-se diretamente ao OPNsense (WAN). Uma bridge secundária (`vmbr3`) opera em modo **VLAN-Aware (802.1Q)** para segmentar as subnets entre cada nó LXC.
*   **Gestão Out-of-Band (OOB):** Isolada numa VLAN específica de gestão para acesso administrativo seguro.

---

## 🌐 Acesso Externo e Conetividade

1.  **Ingress sem Exposição:** Não existem regras de NAT direto (port forwarding) na WAN pública. Todo o tráfego de entrada legítimo (HTTP/HTTPS) é encaminhado através de ligações de saída (Outbound) estabelecidas por um daemon do **Cloudflare Tunnel** até ao proxy reverso interno.
2.  **Rede Mesh Segura:** O acesso administrativo remoto e interligação de nós faz-se através do **Netbird**, uma VPN em malha baseada no protocolo WireGuard.

---

## 🗺️ Diagrama de Arquitetura

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
        NIC0[Interface Física nic0]:::hardware
        
        subgraph V_SWITCH [Switch Virtual - VLAN-Aware]
            VMBR0[vmbr0: WAN Bridge]:::network
            VMBR3[vmbr3: VLAN Trunk]:::network
            VMBR90[VLAN Management]:::network
        end

        OPNSENSE{Firewall OPNsense}:::gateway

        subgraph COMPUTE [Nós LXC]
            direction LR
            Node1[LXC Proxy]:::lxc
            Node2[LXC IAM Core]:::lxc
            Node3[LXC Media]:::lxc
            Node4[LXC Serviços Privados]:::lxc
        end

        subgraph WORKLOADS [Serviços Docker]
            S_Traefik([Traefik]):::svc
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

## 🛠️ Especificação dos Nós LXC

*   **Nó Proxy (Edge Routing):** Responsável por fazer a terminação TLS, renovação de certificados DNS-01 e proxy de tráfego. Corre **Traefik** e **Cloudflared**.
*   **Nó IAM Core (Segurança e Identidade):** Centralização de credenciais, provedor OIDC/SAML e VPN. Corre **Authentik** e o cliente **Netbird**.
*   **Nó Media (Multimédia e Automação):** Gerenciamento e streaming de conteúdo. Corre **Jellyfin** (com transcodificação por hardware via passthrough de GPU integrado) e a stack de aquisição de média.
*   **Nó Serviços Privados (Dados & Observabilidade):** Armazenamento de ficheiros, stack de inteligência artificial local e telemetria. Corre **Nextcloud**, **Immich**, **Forgejo Git**, **Open-WebUI** e a stack de SRE (**Loki / Grafana / Alloy**).
