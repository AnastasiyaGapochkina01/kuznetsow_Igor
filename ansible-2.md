1) Написать роль для установки и настройки nginx
- установить пакет не из дефолтного репозитория, а из репозитория nginx заданной версии (версию задать в vars)
- сгенерировать конфигурационный файл для web-приложения из шаблона: 
  - http_port - порт для прослушивания по http (по умолчанию 80)
  - https_port - порт для прослушивания по https (по умолчанию 443)
  - docroot - корневой каталог web-приложения
  - app_name - доменное имя web-приложения (по умолчанию webapp.local)
- при изменении конфига nginx запускать релоад
- копировать конфиг для сбора статистики nginx (подробнее [тут](https://www.tecmint.com/enable-nginx-status-page/))
```
server {
  server_name st.local;
  listen 82;

  location /nginx_status {
    stub_status on;
    allow 127.0.0.1;
    deny all;
  }
}
```
2) Написать роль для настройки правил iptables:
- проверить, установлен ли пакет iptables, если нет, то установить
- любым способом (файл или шаблон) реализовать правила
  - разрешить доступ по ssh всем
  - запретить доступ по порту 82 всем, кроме локалхоста
3) Написать роль для установки rabbitmq. Усложнить роль, реализовав настройку [HA-кластера](https://www.rabbitmq.com/docs/clustering) rabbitmq
4) Написать роль для установки Jenkins и jenkins-agent
5) Написать роль для установки и настройки ftp-сервера
6) Написать роль для установки wordpress (на базе nginx и mysql)
