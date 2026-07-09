# 📸 Screenshots

В данной папке находятся скриншоты работы системы мониторинга **Prometheus + Grafana + Node Exporter**.

Скриншоты демонстрируют:

* работу Grafana dashboards;
* состояние Prometheus targets;
* выполнение PromQL запросов;
* проверку Alert Rules.

---

# 📊 Grafana Dashboards

## CPU

Файл:

```
cpu.png
```

Dashboard показывает загрузку процессора Linux-сервера.

Используется метрика:

```promql
node_cpu_seconds_total
```

Отображает:

* текущую загрузку CPU;
* изменение нагрузки во времени;
* состояние системы при высокой нагрузке.

---

## Memory

Файл:

```
memory.png
```

Dashboard показывает использование оперативной памяти.

Используемые метрики:

```promql
node_memory_MemAvailable_bytes

node_memory_MemTotal_bytes
```

Отображает:

* общий объём памяти;
* используемую память;
* процент загрузки RAM.

---

## Disk

Файл:

```
disk.png
```

Dashboard показывает состояние файловой системы.

Основной контролируемый раздел:

```
/
```

Используемые метрики:

```promql
node_filesystem_avail_bytes

node_filesystem_size_bytes
```

Отображает:

* общий размер диска;
* свободное место;
* процент заполнения.

---

## Network

Файлы:

```
network_rx.png
network_tx.png
```

Dashboard показывает сетевую активность сервера.

Отображает:

* входящий трафик (RX);
* исходящий трафик (TX).

Используемые метрики:

```promql
node_network_receive_bytes_total

node_network_transmit_bytes_total
```

---

# 🔎 Prometheus

## Targets

Файл:

```
prometheus_targets.png
```

Показывает состояние подключенных targets.

В проекте используется:

```
VM1 Node Exporter :9100
```

Статусы:

```
UP   — target доступен

DOWN — target недоступен
```

---

## UP Metric

Файл:

```
prometheus_up_query.png
```

Проверка доступности сервера через метрику:

```promql
up
```

Используется для создания:

```
Host Down Alert
```

---

# 🚨 Alert Testing

В данной папке находятся скриншоты проверки Alert Rules.

Проверенные сценарии:

* Host Down;
* CPU Usage;
* Memory Usage;

Жизненный цикл Alert:

```
Normal → Pending → Firing
```

---

## Host Down

Файл:

```
alerts/host_down_firing.png
```

Проверка выполнялась отключением VM1.

Условие:

```promql
up < 0.5
```

Результат:

```
VM1 недоступна → Alert Firing
```

---

## CPU Alert

Файл:

```
alerts/cpu_alert_firing.png
```

Проверка выполнялась созданием искусственной нагрузки CPU.

Пример:

```bash
stress-ng --cpu 0 --cpu-load 95 --timeout 300s
```

Условие:

```
CPU Usage > 80%
```

---

## Memory Alert

Файл:

```
alerts/memory_alert_firing.png
```

Проверка выполнялась увеличением использования оперативной памяти.

Пример:

```bash
stress --vm 1 --vm-bytes 250M --timeout 180
```

Условие:

```
Memory Usage > 80%
```

---

# 📁 Structure

```
screenshots/

├── cpu.png
├── memory.png
├── disk.png
├── network_rx.png
├── network_tx.png
│
├── prometheus_targets.png
├── prometheus_up_query.png
│
└── alerts/
    ├── host_down_firing.png
    ├── cpu_alert_firing.png
    ├── memory_alert_firing.png
    └── disk_alert_firing.png
```

---

# 🎯 Purpose

Данные скриншоты подтверждают работу системы мониторинга:

* сбор метрик через Node Exporter;
* обработку данных Prometheus;
* визуализацию в Grafana;
* работу Alert Rules.
