# Memory Usage Dashboard

Dashboard показывает использование оперативной памяти Linux-сервера.

Используемые метрики:

```promql
node_memory_MemAvailable_bytes

node_memory_MemTotal_bytes
```

Расчёт процента использования:

```promql
100 * (
1 -
(
node_memory_MemAvailable_bytes
/
node_memory_MemTotal_bytes
)
)
```

Отображаемые данные:

- общий объём RAM;
- доступная память;
- процент использования.

Используется для настройки Memory Alert.

Пример условия:

```
Memory Usage > 80%
```