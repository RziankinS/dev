# Средство визуализации Grafana
### Задание 1

![1](https://github.com/RziankinS/devops-netology/blob/e89839aa8a9ccfc1424399556b2eb4fd96bd054a/screen/grafana/%D0%B2%D0%B5%D0%B1-%D0%B8%D0%BD%D1%82%D0%B5%D1%80%D1%84%D0%B5%D0%B9%D1%81%20grafana%20%D1%81%D0%BE%20%D1%81%D0%BF%D0%B8%D1%81%D0%BA%D0%BE%D0%BC%20%D0%BF%D0%BE%D0%B4%D0%BA%D0%BB%D1%8E%D1%87%D0%B5%D0%BD%D0%BD%D1%8B%D1%85%20Datasource.png)

## Задание 2

![2](https://github.com/RziankinS/devops-netology/blob/e89839aa8a9ccfc1424399556b2eb4fd96bd054a/screen/grafana/dashboard.png)

### Используемые promql-запросы:
```
"node_filesystem_avail_bytes"  -  количество места на файловой системе
"node_filesystem_avail_bytes{device="/dev/nvme1n1p2", fstype="ext4", instance="nodeexporter:9100", job="nodeexporter", mountpoint="/"}" - свободное место по кокретному диску
"node_memory_MemFree_bytes{job='nodeexporter'}" и "node_memory_MemTotal_bytes" -  количество свободной оперативной памяти
"avg by (instance) (irate(node_cpu_seconds_total{mode="idle"}[5m])) * 100"  -  CPULA 1/5/15;
"sum(rate(node_cpu_seconds_total{mode="idle"}[1m])) * 100"  -  утилизация CPU для nodeexporter (в процентах, 100-idle)
```

## Задание 3

![3](https://github.com/RziankinS/devops-netology/blob/e89839aa8a9ccfc1424399556b2eb4fd96bd054a/screen/grafana/alerts.png)

## Задание 4

[test_grafana.json](https://github.com/RziankinS/devops-netology/blob/5ebac94db20466187914f2ae98c037b6df5e9b0b/screen/grafana/test_grafana.json)
