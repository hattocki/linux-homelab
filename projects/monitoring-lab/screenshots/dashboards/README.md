# 📊 Grafana Dashboards Screenshots

В данной папке находятся скриншоты Grafana dashboards, созданных в рамках проекта **Prometheus + Grafana + Node Exporter**.

Скриншоты демонстрируют работу системы мониторинга и визуализацию основных метрик Linux-сервера VM1.

---

# 🖥️ Monitored Metrics

В Grafana были созданы dashboards для следующих системных показателей:

- CPU Usage
- Memory Usage
- Disk Usage
- Network Traffic

Источник данных:


VM1
|
| Node Exporter :9100
|
↓
Prometheus
|
↓
Grafana


---

# 📈 Dashboard Screenshots

## CPU Usage

Файл:


cpu.png


Dashboard отображает загрузку процессора сервера.

Используется для:

- мониторинга текущей нагрузки CPU;
- анализа изменения нагрузки во времени;
- проверки работы CPU Alert.

---

## Memory Usage

Файл:


ram.png


Dashboard отображает использование оперативной памяти.

Показывает:

- общий объём памяти;
- используемую память;
- процент загрузки RAM.

Используется для:

- контроля состояния памяти;
- проверки Memory Alert.

---

## Disk Usage

Файл:


disk_usage.png


Dashboard отображает состояние файловой системы.

Контролируемый раздел:


/


Показывает:

- общий размер диска;
- занятое пространство;
- процент заполнения.

Используется для:

- контроля свободного места;
- проверки Disk Alert.

---

## Network Traffic

Файлы:


network_rx.png
network_tx.png


Dashboard отображает сетевую активность сервера.

RX:

- входящий сетевой трафик.

TX:

- исходящий сетевой трафик.

Используется для анализа:

- сетевой нагрузки;
- изменения количества передаваемых данных.

---

# 🎯 Purpose

Данные скриншоты подтверждают:

- успешный сбор метрик через Node Exporter;
- подключение Prometheus datasource;
- корректную работу Grafana dashboards;
- визуализацию состояния Linux-сервера.

---

# 📁 Structure


dashboards/

├── README.md
├── cpu.png
├── ram.png
├── disk_usage.png
├── network_rx.png
└── network_tx.png