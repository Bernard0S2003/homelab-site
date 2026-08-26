# 🚀 Projetos & Práticas DevOps

Visão geral dos processos de engenharia, controlo de alterações e planeamento de projetos em curso no homelab.

---

## ⚙️ CI/CD & Gestão IaC (GitOps)

Para evitar configurações manuais e inconsistências (*configuration drift*), a gestão da infraestrutura é tratada como código (Infrastructure as Code):

*   **Versionamento Centralizado:** Todos os ficheiros Docker Compose e blueprints de configuração do Proxmox e OPNsense são guardados em repositórios privados na instância local do **Forgejo**.
*   **Procedimento de Alterações:** Todo os upgrades ou spins de novos serviços são desenhados de forma declarativa e documentados, permitindo uma reconstrução completa (Disaster Recovery) a partir dos ficheiros lidos no repositório com poucos comandos.

---

## 🛡️ Pipelines de Salvaguarda (Backups)

*   **Kopia Backup Engine:** Encriptação na origem, compressão e deduplicação de dados de configuração dos contentores. Os backups gerados são enviados sob agendamento cronometrado para repositórios isolados locais e em clouds externas.
*   **Snapshots Proxmox (PBS):** Salvaguarda programada de backups das máquinas virtuais e contentores LXC do Proxmox VE ao nível de bloco.

---

## 🔮 Roteiro Operacional (Roadmap Público)

### Automações Core & IaC
- [x] Unificação de domínios internos e terminação TLS automática via DNS Challenge no Traefik.
- [x] Centralização integrada de logs críticos e alertas via Slack ou Discord.
- [ ] Implementação de provisionamento e automação de máquinas via Ansible.
- [ ] Migração controlada da gestão de containers remotos para Portainer com GitOps.

### Robustez & Segurança
- [x] Integração de SSO via Authentik com múltiplos fatores de autenticação (MFA).
- [ ] Construção de um laboratório de Staging baseado em Proxmox Linked Clones para validação de alterações de software (Remediação Baseada em Testes).
