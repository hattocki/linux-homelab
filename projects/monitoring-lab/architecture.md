# Monitoring Architecture

## Overview

This lab demonstrates a simple monitoring system.

## Components

### VM1 (Target)
- Node Exporter
- Exposes system metrics on port 9100

### VM2 (Monitoring Server)

- Prometheus:
  - scrapes metrics from VM1
  - stores time-series data

- Grafana:
  - visualizes metrics from Prometheus

## Data Flow

node_exporter (VM1)
        ↓
   Prometheus (VM2)
        ↓
     Grafana (VM2)

## Ports

- 9100 → Node Exporter
- 9090 → Prometheus
- 3000 → Grafana