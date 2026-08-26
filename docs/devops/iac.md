# 🛠️ Infraestrutura como Código (IaC)

A filosofia do Homelab assenta na máxima **"Tratar servidores como gado, não como animais de estimação"** (*Cattle, not pets*). O estado dos servidores é gerido de forma declarativa e automatizada.

---

## 📜 Ansible

O Ansible é utilizado para a configuração base de novos nós e máquinas virtuais:

- Atualização periódica de pacotes de segurança nos nós Linux (`apt update && apt upgrade`).
- Instalação e configuração padronizada de Docker, Docker Compose e ferramentas CLI (`btop`, `zsh`, `curl`, `git`).
- Configuração de utilizadores, chaves SSH autorizadas e regras de firewall UFW.

### Exemplo de Playbook Estruturado:
```yaml
---
- name: Setup base de nós Linux
  hosts: servers
  become: true
  roles:
    - common_packages
    - security_hardening
    - docker_engine
```

---

## 🧩 Docker Compose & GitOps

- Todos os serviços são versionados num repositório Git.
- Separação entre ficheiros de template (`compose.yaml`) e ficheiros locais de ambiente (`.env`).
