## Теория
1) [Введение в YCloud](https://youtu.be/cTMvb-0kibA)
2) [Начало работы с TF](https://youtu.be/AwTc65TOjpQ)

## Практика
1) С помощью TF поднять машины
- pg-main с параметрами
  - 2 cpu
  - 4 mem
  - добавить дополнительный диск pg-data
- ws-1 с параметрами
  - 2 cpu
  - 2 mem
- app-server-1 с такими же параметрами как ws-1
2) На хосты с помощью ролей ansible установить
- на pg-main - postgres
- на ws-1 - nginx
- на app-server-1 - docker
Очень хорошо сделать одним плейбуком и в зависимости от роли хоста катать там соответствующую роль ansible

Совместно TF и ansible пока не используем
