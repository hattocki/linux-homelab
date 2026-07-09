# Network Dashboard

Dashboard предназначен для мониторинга сетевой активности сервера.

Используемые метрики:

Получение данных:

```promql
rate(node_network_receive_bytes_total[1m])
```

Передача данных:

```promql
rate(node_network_transmit_bytes_total[1m])
```

Отображаемые показатели:

- входящий трафик;
- исходящий трафик;
- изменение нагрузки сети во времени.