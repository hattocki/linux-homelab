# 🛠 Troubleshooting

This document describes issues encountered during setup of the monitoring stack and their resolution.

---

## Node Exporter service not starting after reboot

### Description
Node Exporter was installed, but did not start automatically after system reboot.

### Resolution
The systemd service was enabled to ensure automatic startup:

```bash
sudo systemctl enable node_exporter
sudo systemctl start node_exporter
```

Service status verified with:

```bash
systemctl status node_exporter
```

---

## Prometheus target unavailable (DOWN state)

### Description
Prometheus showed the monitored host as unavailable.

### Investigation
Connectivity between Prometheus and Node Exporter was verified:

```bash
curl http://<VM1_IP>:9100/metrics
```

### Resolution
Prometheus configuration was updated to ensure correct target definition:

```yaml
scrape_configs:
  - job_name: "vm1"
    static_configs:
      - targets: ["192.168.56.101:9100"]
```

---

## Grafana dashboards showing no data

### Description
Grafana panels did not display metrics.

### Resolution
- Verified Prometheus datasource configuration
- Ensured Prometheus was reachable from Grafana
- Validated queries in Explore mode

Example test query:

```promql
up
```

---

## PromQL query returned empty results

### Description
Certain metrics did not return data when queried directly.

### Resolution
Correct query type usage was applied for counter metrics:

```promql
rate(node_cpu_seconds_total[1m])
```

---

## Key notes

- Always verify service status via systemd
- Ensure network connectivity between monitoring components
- Validate PromQL expressions based on metric type
- Use Grafana Explore for query debugging