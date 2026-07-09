# Архитектура системы мониторинга

## Общая схема

VM1 → Node Exporter → Prometheus → Grafana

## Компоненты

## VM1
- Ubuntu
- Node Exporter
- порт 9100

## VM2
- Ubuntu
- Prometheus
- Grafana

## Поток данных

1. Node Exporter собирает метрики
2. Prometheus выполняет scrape
3. Grafana получает данные из Prometheus
4. Alert Rules проверяют условия

## Используемые порты

| Сервис | Порт |
|---|---|
| Node Exporter | 9100 |
| Prometheus | 9090 |
| Grafana | 3000 |