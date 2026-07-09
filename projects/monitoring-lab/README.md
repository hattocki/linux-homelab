# 📊 Система мониторинга Linux-серверов (Prometheus + Grafana + Node Exporter)

## 📌 Описание проекта

В рамках проекта была развернута система мониторинга Linux-виртуальных машин на базе:

- Node Exporter
- Prometheus
- Grafana

Цель проекта:

- изучить принципы построения системы мониторинга;
- научиться собирать системные метрики;
- разобраться с PromQL;
- настроить визуализацию состояния серверов;
- реализовать автоматические оповещения при возникновении проблем.

---

# 🏗 Архитектура проекта

```
VM1 (Ubuntu)
│
└── Node Exporter :9100
    │
    │ Сбор системных метрик
    │
    ↓

VM2 (Ubuntu)

├── Prometheus :9090
│   │
│   └── Сбор и хранение временных рядов
│
└── Grafana :3000
    │
    └── Dashboards + Alert Rules
```

---

# 🖥 Инфраструктура

## VM1 — контролируемый сервер

Назначение:

- тестовая Linux-виртуальная машина;
- источник системных метрик.

Установленный компонент:

## Node Exporter

Node Exporter используется для сбора информации о состоянии Linux-системы.

Собираемые показатели:

- загрузка CPU;
- использование оперативной памяти;
- состояние дисковой подсистемы;
- сетевой трафик;
- доступность сервера.

Порт:

```
9100
```

Особенности настройки:

- создан systemd service;
- включён автозапуск;
- настроен restart при сбое.

---

# VM2 — сервер мониторинга

Назначение:

- сбор метрик;
- хранение временных рядов;
- визуализация данных;
- настройка автоматических оповещений.

---

# Prometheus

Prometheus используется для:

- получения метрик от Node Exporter;
- хранения временных рядов;
- выполнения PromQL запросов;
- проверки состояния targets.

Порт:

```
9090
```

---

# Grafana

Grafana используется для:

- создания dashboards;
- визуализации состояния серверов;
- настройки Alert Rules.

Порт:

```
3000
```

Созданные dashboards:

- CPU Usage;
- Memory Usage;
- Disk Usage;
- Network Traffic.

---

# 📈 Собираемые метрики

## CPU

Контроль загрузки процессора.

Используется для:

- анализа нагрузки;
- настройки CPU Alert.

---

## Memory

Контроль использования оперативной памяти.

Отслеживаются:

- общий объём памяти;
- доступная память;
- процент использования.

---

## Disk

Контроль заполненности файловой системы.

Мониторится:

```
/
```

корневой раздел Linux.

---

## Network

Контроль:

- входящего трафика;
- исходящего трафика.

---

## System Availability

Используется встроенная метрика Prometheus:

```promql
up
```

Позволяет определить доступность сервера.

---

# 🚨 Настроенные Alert Rules

В Grafana были созданы правила автоматического оповещения.

---

## CPU Usage Alert

Условие:

```
CPU Usage > 80%
```

Время подтверждения:

```
For: 1 минута
```

---

## Memory Usage Alert

Условие:

```
Memory Usage > 80%
```

Время подтверждения:

```
For: 1 минута
```

---

## Disk Usage Alert

Контролируемый раздел:

```
/
```

Условие:

```
Disk Usage > 85%
```

---

## Host Down Alert

Используемая метрика:

```promql
up
```

Логика:

```
1 — сервер доступен

0 — сервер недоступен
```

Условие:

```
up < 0.5
```

При потере связи с Node Exporter сервер считается недоступным.

---

# 🔎 Используемые PromQL запросы

## Проверка доступности сервера

```promql
up
```

---

## Использование CPU

```promql
100 - (
avg by(instance)
(rate(node_cpu_seconds_total{mode="idle"}[1m]))
* 100
)
```

---

## Использование памяти

```promql
100 * (
1 -
(
node_memory_MemAvailable_bytes{job="vm1"}
/
node_memory_MemTotal_bytes{job="vm1"}
)
)
```

---

## Использование диска

```promql
100 * (
1 -
(
node_filesystem_avail_bytes{
job="vm1",
mountpoint="/",
fstype!="tmpfs",
fstype!="overlay"
}
/
node_filesystem_size_bytes{
job="vm1",
mountpoint="/",
fstype!="tmpfs",
fstype!="overlay"
}
)
)
```

---

# 🔧 Решённые проблемы

## Alert Memory не срабатывал

### Проблема

При создании нагрузки значение памяти превышало установленный порог, но Alert не переходил в Firing.

### Причина:

- несколько targets возвращали метрики;
- отсутствовала фильтрация по labels;
- учитывались разные источники данных.

### Решение:

Добавлена фильтрация:

```promql
{job="vm1"}
```

---

# Disk Alert показывал некорректные значения

### Проблема:

Prometheus возвращал данные по нескольким файловым системам:

- /
- tmpfs
- /run
- дополнительные mountpoint

### Решение:

Добавлена фильтрация:

```promql
mountpoint="/"
```

---

# Проверка Host Down Alert

Проверка выполнялась:

- остановкой Node Exporter;
- выключением виртуальной машины.

До отключения:

```
up = 1
```

После отключения:

```
up = 0
```

Alert успешно переходил:

```
Normal → Pending → Firing
```

---

# 🧠 Полученные навыки

В ходе работы были изучены:

- Linux administration;
- systemd;
- управление сервисами Linux;
- Node Exporter;
- Prometheus;
- Grafana;
- PromQL;
- Labels:
  - job;
  - instance;
  - mountpoint;
- настройка Alert Rules;
- диагностика проблем мониторинга.

---

# 📂 Структура проекта

```
monitoring-lab/

├── README.md
├── architecture.md
├── troubleshooting.md
├── configs/
├── dashboards/
├── screenshots/
├── vm1/
└── vm2/
```

---

# 📸 Скриншоты

## Grafana Dashboards

- CPU Dashboard
- Memory Dashboard
- Disk Dashboard
- Network Dashboard


## Prometheus

- Targets
- PromQL queries


## Alerts

- CPU Alert
- Memory Alert
- Disk Alert
- Host Down Alert

---

# 📌 Статус проекта

✅ Node Exporter настроен  
✅ Prometheus собирает метрики  
✅ Grafana подключена к Prometheus  
✅ Dashboards созданы  
✅ Alert Rules настроены  
✅ Проверена работа уведомлений  
✅ Проведена диагностика проблем мониторинга  

---

# 👨‍💻 Автор Zaurbek Uzhakhov

DevOps Homelab Project
