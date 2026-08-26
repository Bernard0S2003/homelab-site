# Documentação Pública (GitBook/Site)

Esta pasta contém apenas o conteúdo que será renderizado no site público.

## Como publicar no GitHub Pages
1. Copia o conteúdo desta pasta (`/public-docs`) para a raiz de um novo repositório no GitHub (ex: `homelab-site`).
2. Mantém o ficheiro `mkdocs.yml` na raiz desse novo repositório.
3. No GitHub, vai a **Settings > Pages** e seleciona **Deploy from a branch** (usando GitHub Actions).
4. O GitHub detetará automaticamente o `mkdocs.yml` e compilará o site.

## Estrutura
- `mkdocs.yml`: Configuração do tema e navegação.
- `docs/`: Onde deves adicionar os novos ficheiros Markdown.
