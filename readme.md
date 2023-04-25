Развёртываем связку из Prometheus и Grafana


Порядок работ:

Устанавливаем компонент node_exporter, из него Prometheus будкт получать метрики:
Берём из https://github.com/prometheus/node_exporter/releases распаковываем и копируем /node_exporter в /usr/local/bin/ 
Создаем юнит /etc/systemd/system/node_exporter.service
Запускаем демона:
sudo systemctl daemon-reload && sudo systemctl start node_exporter && sudo systemctl enable node_exporter
Можно проверить отдачу метрик командой curl 'localhost:9100/metrics'
Его Веб-интерфейс будет на порту 9100
Устанавливаем Prometheus:
Качаем пакет из https://github.com/prometheus/prometheus/releases
Распаковываем и копируем /prometheus и /promtool в /usr/local/bin/
/consoles/ в /etc/prometheus/consoles
Создаем /etc/systemd/system/prometheus.service
Запускаем Prometheus
sudo systemctl start prometheus && sudo systemctl enable prometheus
Можно проверить отдачу метрик командой curl 'localhost:9090/metrics'
Веб-интерфейс будет на порту 9090

Установка Grafana:

Качаем пакет из https://grafana.com/grafana/download (нужен VPN)
Устанавливаем и запускам:
sudo apt install ./grafana-enterprise_9.4.7_amd64.deb && sudo systemctl start grafana-server && sudo systemctl enable grafana-server

Сервер поднимается на порту 3000, логин и пароль по умолчанию admin admin
Далее нужно настроить источник данных на Prometheus: http://localhost:9090 и импортировать dashboard, я использовал Node Exporter Full


