# Disk Usage Dashboard

Dashboard используется для мониторинга заполненности файловой системы.

Основной контролируемый раздел:

```
/
```

Используемые метрики:

```promql
node_filesystem_avail_bytes

node_filesystem_size_bytes
```

Расчёт:

```promql
100 * (
1 -
(
node_filesystem_avail_bytes
/
node_filesystem_size_bytes
)
)
```

Дополнительно используется фильтрация:

```promql
mountpoint="/"
```

Исключаются временные файловые системы:

```promql
fstype!="tmpfs"

fstype!="overlay"
```

Используется для настройки Disk Alert.