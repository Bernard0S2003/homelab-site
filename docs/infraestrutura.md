# 🖥️ Infraestrutura & Rede

Visão simples do hardware e da organização da rede.

---

## 🗄️ Hardware

| Equipamento | Função | Specs |
| :--- | :--- | :--- |
| **Servidor Principal** | Hypervisor Proxmox VE | *(Ex: Intel i5 / 32GB RAM / 1TB SSD)* |
| **Storage / NAS** | Armazenamento & Partilhas | *(Ex: 2x 4TB HDD / ZFS)* |
| **Router / Switch** | Gestão de rede e firewall | *(Ex: Mini PC / Switch Gigabit)* |

---

## 🌐 Rede & Acessos

- **Isolamento de Rede:** Separação entre dispositivos normais, servidores e IoT.
- **Acesso Remoto:** Feito de forma segura através de VPN (Tailscale / WireGuard), sem portas desnecessárias abertas na internet.
- **DNS Local:** Bloqueio de anúncios e resolução de nomes locais (AdGuard Home / Pi-hole).
