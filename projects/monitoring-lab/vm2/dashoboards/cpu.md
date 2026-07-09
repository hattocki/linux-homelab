# CPU Usage Dashboard

Dashboard предназначен для мониторинга загрузки процессора Linux-сервера.

Используемая метрика:

```promql
node_cpu_seconds_total
```

Основной запрос:

```promql
100 - (
avg by(instance)
(rate(node_cpu_seconds_total{mode="idle"}[1m]))
* 100
)
```

Отображаемые данные:

- текущая загрузка CPU;
- изменение нагрузки во времени;
- выявление высокой загрузки процессора.

Используется для настройки CPU Alert.

Пример условия:

```
CPU Usage > 80%
```