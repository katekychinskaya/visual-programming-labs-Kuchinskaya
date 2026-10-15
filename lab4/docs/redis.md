# Redis в n8n — лабораторная 4, часть 3

## Что сделано

Настроена интеграция n8n с Redis для сохранения, чтения и удаления ключей.

## Установка Redis

Redis запущен в Docker:
docker run -d --name redis -p 6379:6379 redis:7
- **Образ:** `redis:7`
- **Порт:** `6379`
- **Контейнер:** `redis`

## Настройка credentials в n8n

Созданы Redis credentials:

- **Credential name:** `Redis Local`
- **Host:** `host.docker.internal`
- **Port:** `6379`
- **Database:** `0`
- **Password:** (пусто)

`host.docker.internal` — это специальный адрес, по которому контейнер n8n видит **хост-машину** (Windows) и, соответственно, Redis.

## Workflow A: Set + Get

**Файл:** `flow-09-redis.json`

**Схема:** `Manual Trigger → Redis (Set) → Redis (Get)`

1. **Redis Set** — сохраняет ключ `kuchinskaya` со значением `Привет из n8n, lab4!`
2. **Redis Get** — читает этот ключ

**Результат:** ключ сохранён и прочитан обратно — Output показывает значение.

**Скриншот:** `09-redis-set-get.png`

## Workflow B: Delete + Check

**Файл:** `flow-10-redis.json`

**Схема:** `Manual Trigger → Redis (Delete) → Redis (Get)`

1. **Redis Delete** — удаляет ключ `kuchinskaya`
2. **Redis Get** — пытается прочитать удалённый ключ

**Результат:** Output показывает `null` — ключа больше нет.

**Скриншот:** `10-redis-delete.png`

## Проверка

1. Запустить **Workflow A** → ключ создаётся, читается значение
2. Запустить **Workflow B** → ключ удаляется, чтение возвращает `null`

## Скриншоты

- `08-redis-credentials.png` — настройка credentials
- `09-redis-set-get.png` — Set + Get
- `10-redis-delete.png` — Delete + check (null)
