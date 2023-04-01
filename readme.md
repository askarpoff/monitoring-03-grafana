# Домашнее задание к занятию 14 «Средство визуализации Grafana»

## Обязательные задания

### Задание 1

1. Используя директорию help внутри этого домашнего задания, запустите связку prometheus-grafana.
2. Зайдите в веб-интерфейс grafana, используя авторизационные данные, указанные в манифесте docker-compose.
3. Подключите поднятый вами prometheus, как источник данных.
4. Решение домашнего задания — скриншот веб-интерфейса grafana со списком подключенных Datasource.

## Ответ:
![image](https://user-images.githubusercontent.com/108946489/229273540-1c3a4e6e-6517-45b2-a402-483a914ac301.png)

## Задание 2

Изучите самостоятельно ресурсы:

1. [PromQL tutorial for beginners and humans](https://valyala.medium.com/promql-tutorial-for-beginners-9ab455142085).
2. [Understanding Machine CPU usage](https://www.robustperception.io/understanding-machine-cpu-usage).
3. [Introduction to PromQL, the Prometheus query language](https://grafana.com/blog/2020/02/04/introduction-to-promql-the-prometheus-query-language/).

Создайте Dashboard и в ней создайте Panels:

- утилизация CPU для nodeexporter (в процентах, 100-idle);

`avg by(instance)(rate(node_cpu_seconds_total{mode="idle"}[$__rate_interval])) * 100`

- CPULA 1/5/15;

`avg by (instance)(rate(node_load1{}[$__rate_interval]))`
`avg by (instance)(rate(node_load5{}[$__rate_interval]))`
`avg by (instance)(rate(node_load15{}[$__rate_interval]))`

- количество свободной оперативной памяти;

`node_memory_MemFree_bytes{job="nodeexporter"} / 1024 ^ 3`

- количество места на файловой системе.

`node_filesystem_avail_bytes{instance="nodeexporter:9100",job="nodeexporter",device='/dev/sda1'}/1024^3`

Для решения этого задания приведите promql-запросы для выдачи этих метрик, а также скриншот получившейся Dashboard.
![image](https://user-images.githubusercontent.com/108946489/229307373-b02599b4-e820-44b4-9a3b-1cbe1afd8c74.png)

## Задание 3

1. Создайте для каждой Dashboard подходящее правило alert — можно обратиться к первой лекции в блоке «Мониторинг».
2. В качестве решения задания приведите скриншот вашей итоговой Dashboard.

## Задание 4

1. Сохраните ваш Dashboard.Для этого перейдите в настройки Dashboard, выберите в боковом меню «JSON MODEL». Далее скопируйте отображаемое json-содержимое в отдельный файл и сохраните его.
2. В качестве решения задания приведите листинг этого файла.

---
