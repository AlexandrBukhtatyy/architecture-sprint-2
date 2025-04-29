# pymongo-api

## Как запустить

**ВНИМАНИЕ !**<br/>
В Windows команды нужно запускать из git bash

Запускаем mongodb и приложение

```shell
# Запуск сервисов
docker compose up -d

# Настройка сервера конфигурации
bash ./scripts/init-mongo-configuration-server.sh configSrv 27017

# Настройка шардов
bash ./scripts/init-mongo-shard.sh shard1 27018
bash ./scripts/init-mongo-shard.sh shard2 27019

# Настройка роутеров
bash ./scripts/init-mongo-router.sh mongos_router1 27020
bash ./scripts/init-mongo-router.sh mongos_router2 27020

# Заполнение данными роутеров
bash ./scripts/seed-mongo-db.sh mongos_router1 27020
bash ./scripts/seed-mongo-db.sh mongos_router2 27020

#Проверка шардов на заполнение
bash ./scripts/check-mongo-shard.sh shard1 27018 # В ответе дожно быть: 984
bash ./scripts/check-mongo-shard.sh shard2 27019 # В ответе дожно быть: 1016
```

## Как Остановить

```shell
# Остановка приложения и зачистка ресурсов
docker compose down --remove-orphans --volumes
```

## Как проверить

### Если вы запускаете проект на локальной машине

Откройте в браузере http://localhost:8080

### Если вы запускаете проект на предоставленной виртуальной машине

Узнать белый ip виртуальной машины

```shell
curl --silent http://ifconfig.me
```

Откройте в браузере http://<ip виртуальной машины>:8080

## Доступные эндпоинты

Список доступных эндпоинтов, swagger http://<ip виртуальной машины>:8080/docs