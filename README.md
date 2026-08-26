# 🌐 Homelab Documentation & Portfolio

Repositório com o código-fonte e documentação do meu **Homelab**, publicado automaticamente no **GitHub Pages** via **MkDocs Material**.

---

## 🚀 Como testar localmente

Se quiseres pré-visualizar o site localmente com live-reload:

```bash
# 1. Instalar as dependências
pip install mkdocs-material

# 2. Iniciar o servidor de desenvolvimento
mkdocs serve
```

Acede a `http://127.0.0.1:8000` no teu browser.

---

## 📁 Estrutura do Repositório

```text
├── .github/workflows/       # Pipeline CI/CD de deploy automático no GitHub Pages
├── docs/                    # Todo o conteúdo em Markdown do site
│   ├── index.md             # Página inicial do portefólio
│   ├── sobre.md             # Perfil e contactos
│   ├── arquitetura/         # Visão geral, VLANs, topologia de rede e segurança
│   ├── infraestrutura/      # Hardware, Proxmox VE, Docker, ZFS e Backups
│   ├── servicos/            # Catálogo de serviços self-hosted e monitorização
│   ├── devops/              # Ansible, Terraform, GitOps e CI/CD
│   └── projetos/            # Guias passo-a-passo e roadmap futuro
├── mkdocs.yml               # Configuração do MkDocs (tema Material, navegação, plugins)
└── README.md                # Este ficheiro
```

---

## 🔄 Deploy Contínuo

O deploy é gerido automaticamente pelo GitHub Actions a cada `push` na branch `main`.
