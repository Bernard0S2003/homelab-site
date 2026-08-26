# 🔒 Segurança & Acessos

Estratégia e camadas de proteção adotadas no Homelab para garantir a integridade dos serviços internos e a segurança das ligações remotas.

---

## 🛡️ Camadas de Defesa

### 1. Acesso Remoto Seguro
- **VPN Mesh (Tailscale / WireGuard):** Não há portas de gestão (SSH, Proxmox, Portainer) abertas diretamente na WAN. Todo o acesso administrativo fora de casa é feito via VPN cifrada ponto-a-ponto.
- **Cloudflare Tunnels:** Utilizado pontualmente para expor aplicações públicas específicas sem necessidade de abrir portas no router residencial (`Port Forwarding`).

### 2. Reverse Proxy & Certificados SSL/TLS
- **Nginx Proxy Manager / Traefik:** Centraliza a terminação SSL, gestão de certificados automáticos via Let's Encrypt / ACME e redirecionamentos HTTPS obrigatórios.
- **Headers de Segurança:** Implementação de HSTS, CSP e proteção contra clickjacking.

### 3. Autenticação Centralizada & 2FA
- **Authelia / Authentik:** Proteção de serviços que não possuem autenticação nativa através de autenticação multifator (MFA / TOTP / FIDO2).

### 4. Hardening de Servidores
- Chaves SSH obrigatórias (login por password desativado).
- **Fail2ban / CrowdSec:** Deteção e bloqueio de tentativas de força bruta.
- Atualizações automáticas de segurança (*unattended-upgrades*).
