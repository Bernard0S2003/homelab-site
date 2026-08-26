# 📈 Monitorização & Observabilidade

A infraestrutura possui monitorização contínua de integridade, telemetria e alertas proativos para evitar indisponibilidades.

---

## 🔍 Stack de Observabilidade

```mermaid
flowchart TD
    subgraph Exporters ["Exportadores de Métricas"]
        NodeExp[Node Exporter / Proxmox]
        cAdvisor[cAdvisor / Docker Metrics]
        SNMP[SNMP Exporter / Switch & Router]
    end

    subgraph Core ["Processamento & Armazenamento"]
        Prometheus[(Prometheus TSDB)]
        Loki[(Grafana Loki / Logs)]
    end

    subgraph Visualization ["Visualização & Alertas"]
        Grafana[📊 Grafana Dashboards]
        UptimeKuma[⏱️ Uptime Kuma Status Page]
        Alerts[🔔 Notificações Discord / Telegram]
    end

    Exporters --> Prometheus
    Prometheus --> Grafana
    Prometheus --> Alerts
    UptimeKuma --> Alerts
```

---

## 🔔 Política de Alertas
- **Uptime Kuma:** Testa a cada 60 segundos se as portas e endpoints HTTP estão saudáveis (`200 OK`).
- **Notificações:** Enviadas via webhook para um canal privado do Discord ou Telegram no caso de:
  - Serviço offline há mais de 2 minutos.
  - Uso de disco > 85%.
  - Temperatura de CPU anómala.
