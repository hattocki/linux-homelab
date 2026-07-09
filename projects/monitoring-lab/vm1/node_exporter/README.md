# Node Exporter Service

В данной папке находится systemd unit-файл для запуска Node Exporter на VM1.

Node Exporter используется как агент мониторинга и предоставляет системные метрики Linux для Prometheus.

Файл:

```
node_exporter.service
```

используется systemd для управления сервисом.

Основные функции unit-файла:

- запуск Node Exporter;
- указание пользователя, от которого работает сервис;
- автоматический запуск при загрузке системы;
- перезапуск сервиса при ошибке.

После установки сервис управляется через systemctl:

Проверка статуса:

```bash
systemctl status node_exporter
```

Запуск:

```bash
systemctl start node_exporter
```

Остановка:

```bash
systemctl stop node_exporter
```

Перезапуск:

```bash
systemctl restart node_exporter
```

Проверка автозапуска:

```bash
systemctl is-enabled node_exporter
```