### Задача
Необходимо развернуть сервер мониторинга и логирования на базе PromStack

### Компоненты сервера мониторинга и логирования
- prometheus
- grafana
- alertmanager
- loki
### Требования к реализации
- инфраструктура (сервер) создается с помощью terraform и отдельного инфраструктурного пайплайна CI/CD
- компоненты стека устанавливаются в docker с помощью ansible и terraform provisioner; prometheus и loki подключаются к grafana **автоматически**
- на вируталки приложения добавляются контейнеры с
  - node-exporter
  - cadvisor-exporter
  - postgres-exporter
  - nginx-exporter
  - promtail
