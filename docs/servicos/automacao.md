# 🏡 Automação & Casa Inteligente

Integração de domótica, IoT local e automação residencial sem dependência de clouds externas.

---

## 🛠️ Tecnologias Utilizadas

- **Home Assistant OS / Container:** O cérebro central da casa inteligente.
- **Zigbee2MQTT / Z-Wave JS:** Controlo direto de sensores, interruptores e lâmpadas através de adaptadores USB locais (sem pontes proprietárias).
- **Node-RED:** Criação de fluxos complexos de automação lógica.
- **Mosquitto (MQTT Broker):** Barramento de comunicação leve entre dispositivos e o Home Assistant.

---

## 🔒 Princípios de Segurança em IoT

1. **VLAN Isolada:** Todos os dispositivos inteligentes encontram-se na VLAN de IoT sem acesso à rede de computadores pessoais nem aos servidores de gestão.
2. **Local-First:** Prioridade a dispositivos que funcionem 100% de forma local sem necessidade de acesso à Internet pública.
