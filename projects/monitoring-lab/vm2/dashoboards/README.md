# 📊 Grafana Dashboards

В данной папке описаны dashboards, созданные в Grafana для визуализации состояния Linux-сервера.

Grafana используется как слой визуализации данных, полученных из Prometheus.

Источник данных:

```
Grafana → Prometheus → Node Exporter → Linux Server
```

Созданные dashboards:

- CPU Usage
- Memory Usage
- Disk Usage
- Network Traffic

Каждый dashboard использует PromQL запросы для получения актуальных метрик системы.