# Monitoring Lab (Prometheus + Grafana + Node Exporter)

## 📌 Overview

This project demonstrates a simple monitoring stack using:

- Prometheus (metrics collector)
- Node Exporter (system metrics agent)
- Grafana (visualization)

---

## 🏗 Architecture

VM1 (ubuntu1):
- node_exporter → exposes system metrics on port 9100

VM2 (ubuntu2):
- Prometheus → scrapes metrics from VM1
- Grafana → visualizes data from Prometheus

Flow:

node_exporter → Prometheus → Grafana

---

## 📊 Metrics collected

- CPU usage
- Memory usage
- Disk usage
- Network traffic

---

## 📈 PromQL examples

### CPU usage
100 - (avg by(instance)(rate(node_cpu_seconds_total{mode="idle"}[1m])) * 100)

### Memory usage
100 * (1 - (node_memory_MemAvailable_bytes / node_memory_MemTotal_bytes))

### Disk usage
100 * (1 - (node_filesystem_avail_bytes / node_filesystem_size_bytes))

### Network RX/TX
rate(node_network_receive_bytes_total[1m])
rate(node_network_transmit_bytes_total[1m])

---

## ⚙️ Setup

- node_exporter installed as systemd service
- Prometheus configured via prometheus.yml
- Grafana connected as Prometheus datasource

---

## 🎯 Goal of project

To build a basic production-like monitoring system and understand:

- metrics collection
- time-series monitoring
- visualization dashboards

---

## 👨‍💻 Author

DevOps learning project by hattocki