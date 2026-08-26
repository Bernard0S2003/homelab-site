# 🔄 CI/CD & Automação de Deploys

Pipelines de integração e entrega contínua utilizadas para documentação e serviços do Homelab.

---

## 🚀 GitHub Actions

1. **Deploy deste Site de Portefólio (MkDocs):**
   - A cada `git push` na branch `main`, um runner do GitHub Actions compila o MkDocs Material e publica automaticamente no GitHub Pages.
2. **Linting & Validação:**
   - Validação de sintaxe YAML de ficheiros Compose e Playbooks de Ansible.
3. **Renovate / Dependabot:**
   - Verificação semanal de atualizações de imagens Docker para manter os serviços atualizados com patches de segurança.
