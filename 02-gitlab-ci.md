### Описание задачи
Необходимо создать pipeline, который будет:
- Собирать Docker-образ приложения https://github.com/AnastasiyaGapochkina01/go-http-db
- Развертывать приложение на удаленном сервере с помощью Ansible
- Проверять работоспособность развернутого приложения
### Требования к реализации
1) Docker:
  - делать multistage сборку
  - публиковать собранный image в container registry
  - у БД должен быть healthcheck
  - деплой осуществлять с помощью docker compose, который должен содержать сервисы
    - приложение
    - postgres
    - migrator
    ```
    migrator:
      image: postgres:15
      restart: on-failure
      environment:
        PGPASSWORD: postgres
      volumes:
        - ./migrations:/migrations
      command: >
        sh -c "while ! pg_isready -h db -U postgres; do sleep 1; done && psql -h db -U postgres -d app_db -f /migrations/001_init.sql"
    ```
2) Ansible:
- написать роли для
  - установки docker
  - разворачивания приложения
3) GitLab CI:
- pipeline должен содержать этапы
  - linter (для файлов приложения, файлов docker, файлов ansible)
  - build
  - test (запуск всей инфраструктуры любым способом и простой запрос ```curl http://$host:8080/hello```)
  - deploy
- должно быть ручное подтверждение перед деплоем
