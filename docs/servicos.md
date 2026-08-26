# 📦 Serviços & Stack Tecnológica

Inventário público dos serviços ativos no homelab, organizados pelo seu papel funcional no ecossistema de self-hosting.

---

## 🛡️ Segurança, Rede & Ingress

*   **Traefik Proxy:** Porta de entrada e reverse proxy principal do tráfego interno, responsável pela terminação TLS com certificados obtidos via DNS Challenge.
*   **Netbird:** VPN mesh descentralizada assente em WireGuard. Garante conectividade segura ponto-a-ponto para administração remota sem abrir portas públicas.
*   **Cloudflared:** Daemon do Cloudflare Tunnel. Permite publicar serviços sem mapeamento de portas WAN ou necessidade de IP público estático.
*   **Authentik:** Solução de Identity and Access Management (IAM). Implementa autenticação única (SSO) com múltiplos fatores (MFA) e atua como barreira de segurança (*Forward Auth*) para serviços legados sem suporte nativo a login.

---

## 📊 Observabilidade & Automação SRE

*   **Grafana & Loki:** Stack centralizada de agregação e análise de logs. Permite visualizar e correr queries LogQL sobre o estado operacional de toda a infraestrutura.
*   **Grafana Alloy:** Agente coletor instalado em todos os nós. Efetua a recolha e filtragem bi-direcional de logs dos contentores e recursos de sistema.
*   **Diun (Docker Image Update Notifier):** Analisador passivo de registries. Deteta novas versões das imagens docker em execução e envia notificações para automação do ciclo de atualizações.

---

## 📁 Produtividade & Dados

*   **Nextcloud:** Plataforma modular de alojamento de ficheiros, agenda, contactos e sincronização na cloud privada.
*   **Immich:** Servidor de backup multimédia para recolha de imagens e vídeos de dispositivos móveis. Conta com algoritmos locais de Machine Learning para reconhecimento facial e classificação de cenas.
*   **Forgejo:** Servidor git minimalista hospedado localmente para o controlo de versões, configurações de infraestrutura (IaC) e ferramentas de automação.

---

## 🧠 Inteligência Artificial Local

*   **Open-WebUI:** Interface de chat web adaptada para interação com modelos LLM de inteligência artificial.
*   **Omniroute:** Camada de roteamento e otimização de requisições de IA local e endpoints cloud.

---

## 🎬 Stack de Entretenimento (Media Stack)

*   **Jellyfin:** Servidor multimédia para organização e streaming de vídeo e áudio, com aceleração por hardware GPU ativada.
*   **Pipeline de Aquisição (*arr):** Coleção de utilitários de automação em rede de conteúdo que inclui:
    *   **Sonarr / Radarr:** Gestão e acompanhamento automático de séries e filmes.
    *   **Prowlarr:** Indexador centralizado e gestão de trackers.
    *   **Bazarr:** Sincronizador de legendas multilingue.
    *   **Flaresolverr:** Proxy para resolução de desafios de CDN em requisições web.
