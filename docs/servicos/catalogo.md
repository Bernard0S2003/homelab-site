# 📦 Catálogo de Serviços Self-Hosted

Lista completa de aplicações e serviços em execução no Homelab, categorizados por função.

---

## 🌐 Rede, DNS & Segurança

| Serviço | Tipo | Descrição |
| :--- | :--- | :--- |
| **AdGuard Home / Pi-hole** | Docker / LXC | Servidor DNS local com bloqueio de anúncios e rastreadores |
| **Nginx Proxy Manager / Traefik** | Docker | Reverse Proxy e gestão automática de certificados SSL (Let's Encrypt) |
| **Tailscale / WireGuard** | LXC / Docker | VPN mesh segura para acesso remoto |
| **Authentik / Authelia** | Docker | Autenticação centralizada com suporte para 2FA / SSO |

---

## 📊 Monitorização & Gestão

| Serviço | Tipo | Descrição |
| :--- | :--- | :--- |
| **Uptime Kuma** | Docker | Monitorização de status de serviços e alertas em tempo real |
| **Grafana + Prometheus** | Docker | Métricas de sistema, dashboards de CPU/RAM/Disco e rede |
| **Portainer / Dockge** | Docker | Interface web de gestão e orquestração de containers Docker |
| **Homepage / Dashy** | Docker | Dashboard inicial do Homelab com atalhos e widgets de estado |

---

## 🎬 Media & Entretenimento

| Serviço | Tipo | Descrição |
| :--- | :--- | :--- |
| **Plex / Jellyfin** | Docker | Servidor de streaming de media pessoal |
| **Serviços *arr (Radarr, Sonarr, etc.)** | Docker | Gestão automatizada de biblioteca de media |
| **Transmission / qBittorrent** | Docker | Cliente de downloads associado à VPN |

---

## 🗂️ Produtividade & Utilidades

| Serviço | Tipo | Descrição |
| :--- | :--- | :--- |
| **Nextcloud / Immich** | Docker | Nuvem pessoal de ficheiros e galeria de fotos com IA |
| **Vaultwarden** | Docker | Servidor Bitwarden auto-hospedado para gestão de passwords |
| **Paperless-ngx** | Docker | Digitalização, OCR e arquivo de documentos |
| **IT-Tools** | Docker | Coleção de ferramentas úteis para desenvolvimento e sysadmins |
