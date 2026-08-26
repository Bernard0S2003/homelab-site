# 🖥️ Servidores & Hardware

Inventário do equipamento físico que compõe a infraestrutura do Homelab.

---

## 🗄️ Equipamento Principal

### 🔹 Servidor Principal (Node 01)
- **Função:** Hypervisor Proxmox VE (VMs e Containers de Produção)
- **Chassis/Modelo:** *(Ex: Mini PC / Desktop Custom / 1U Rack)*
- **CPU:** *(Ex: Intel Core i5 / AMD Ryzen 5)*
- **RAM:** *(Ex: 32 GB DDR4)*
- **Armazenamento:** *(Ex: 1x 500GB NVMe SSD OS, 1x 1TB SATA SSD VM Pool)*
- **Rede:** 1GbE / 2.5GbE

### 🔹 Storage / NAS (Node 02)
- **Função:** Armazenamento em rede, backups e partilhas NFS/SMB
- **Chassis/Modelo:** *(Ex: TrueNAS Custom Build / Synology)*
- **CPU:** *(Ex: Intel Celeron / Pentium)*
- **RAM:** *(Ex: 16 GB ECC DDR4)*
- **Pool de Discos:** *(Ex: 2x 4TB HDD em ZFS Mirror / RAID-Z1)*

---

## 🔌 Equipamento de Rede

| Equipamento | Modelo | Função | Portas |
| :--- | :--- | :--- | :--- |
| **Router / Firewall** | *(Ex: OPNsense Mini PC / UniFi)* | Roteamento, Firewall, DHCP, VLANs | 4x 2.5GbE |
| **Switch Gerível** | *(Ex: TP-Link SG108E / UniFi Switch)* | Distribuição de VLANs e trunking | 8x 1GbE |
| **Access Point** | *(Ex: UniFi U6 Lite)* | Wi-Fi com SSIDs mapeados para VLANs | 1x PoE |
| **UPS / No-Break** | *(Ex: APC Back-UPS 700VA)* | Proteção elétrica e encerramento limpo | - |
