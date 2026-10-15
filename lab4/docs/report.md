# Отчёт по лабораторной работе №4. n8n

**Студент:** Кучинская Екатерина  
**Тема:** Освоение n8n как low-code платформы автоматизации  
**Ачивка:** №10 — Redis Pub/Sub

---

## 1. Краткое описание выполненного

В ходе лабораторной работы я установила **n8n** в Docker-контейнере и освоила его как low-code инструмент для визуальной автоматизации. Были собраны и задеплоены **8 основных workflow**, охватывающих базовые и продвинутые ноды, а также настроена интеграция с **Redis** (создание, чтение, удаление ключей). В качестве ачивки реализована передача сообщений между двумя независимыми workflow через **Redis Pub/Sub**.

Все workflow сохранены в папке `lab4/flows/` в виде отдельных JSON-файлов, скриншоты — в `lab4/screenshots/`, документация по Redis — в `lab4/docs/redis.md`.

---

## 2. Способ установки и версии

- **Способ установки:** Docker (образ `n8nio/n8n`)
- **Команда запуска:**
docker run -d --name n8n -p 5678:5678 -v C:\Users\USER\Documents\n8n-data:/home/node/.n8n -v C:\Users\USER\Documents\n8n-data\data:/data n8nio/n8n- **n8n version:** 2.43.4
- **ОС:** Windows 11 Pro, Docker Desktop

---

## 3. Освоенные ноды

| Нода | Что освоила |
|---|---|
| `Manual Trigger` | Ручной запуск workflow |
| `Schedule Trigger` | Запуск по расписанию (каждые 5 минут) |
| `Set (Edit Fields)` | Задание и изменение полей `msg` (payload, topic, timestamp) |
| `Code` | JS-код: `let/const`, `if/else`, цикл `for`, массивы, объекты |
| `IF` | Ветвление по условию |
| `NoOp` | Заглушка (ничего не делать) |
| `HTTP Request` | GET-запросы к публичным API (chucknorris.io) |
| `Redis` | Set/Get/Delete ключей, Publish/Subscribe |
| `Redis Trigger` | Подписка на события Redis (Pub/Sub) |

---

## 4. Ключевые AI-промпты

- «Напиши код для ноды Code в n8n: используй let/const, if/else, цикл for, массив и объект, верни объект с полем payload»
- «Объясни, как в n8n настроить ноду IF для ветвления по значению поля payload.sum»
- «Как настроить HTTP Request в n8n для получения JSON от публичного API?»
- «Как настроить Redis в n8n: credentials, host для Docker-контейнера?»
- «Как реализовать Redis Pub/Sub в n8n — Publisher и Subscriber?»

---

## 5. Все workflow

Все файлы находятся в `lab4/flows/`:

| Файл | Что делает |
|---|---|
| `flow-01-manual-set.json` | Manual → Set → Code |
| `flow-02-code.json` | Manual → Code → NoOp (JS: let/const, if/else, for, массив, объект) |
| `flow-03-if.json` | Manual → Code → IF → (true) NoOp / (false) NoOp |
| `flow-04-set.json` | Manual → Set → Code (payload, topic, timestamp) |
| `flow-05-http.json` | Manual → HTTP Request → Code (API chucknorris.io) |
| `flow-06-schedule.json` | Schedule Trigger → Code (текущее время) |
| `flow-09-redis.json` | Manual → Redis Set → Redis Get |
| `flow-10-redis.json` | Manual → Redis Delete → Redis Get (проверка null) |
| `flow-11-redis-subscribe.json` | Redis Trigger (Subscribe) → NoOp |
| `flow-12-redis-publish.json` | Manual → Redis Publish |

---

## 6. Ачивка №10 — Redis Pub/Sub

**Что сделано:**
- **Workflow 1 (Publisher):** Manual Trigger → Redis Publish → канал `lab4/channel`, сообщение `Привет из Publisher! Кучинская, lab4`
- **Workflow 2 (Subscriber):** Redis Trigger (Subscribe) → NoOp → слушает канал `lab4/channel`

**Как работает:**
1. Subscriber запускается и ждёт сообщения
2. Publisher публикует сообщение в канал
3. Subscriber ловит сообщение и передаёт его в NoOp
4. В Output видно: `channel: lab4/channel`, `message: Привет из Publisher! Кучинская, lab4`

**Скриншоты:** `11-redis-publisher.png`, `11b-redis-subscriber.png`, `11c-redis-subscriber-message.png`

---

## 7. Скриншоты всех workflow

| Файл | Что на нём |
|---|---|
| `01-version.png` | Версия n8n |
| `01-welcome.png` | Приветственный экран |
| `02-2.1-manual-set-code.png` | Workflow 2.1 |
| `03-2.2-code.png` | Workflow 2.2 |
| `04-2.3-if.png` | Workflow 2.3 |
| `05-2.4-set.png` | Workflow 2.4 |
| `06-2.5-http.png` | Workflow 2.5 |
| `07-2.6-schedule.png` | Workflow 2.6 |
| `08-redis-credentials.png` | Redis credentials |
| `09-redis-set-get.png` | Redis Set+Get |
| `10-redis-delete.png` | Redis Delete+Check |
| `11-redis-publisher.png` | Publisher (ачивка) |
| `11b-redis-subscriber.png` | Subscriber (ачивка) |
| `11c-redis-subscriber-message.png` | Пойманное сообщение (ачивка) |

---

## 8. Выводы

В ходе лабораторной работы я освоила **n8n** как low-code платформу для автоматизации. Научилась:
- устанавливать n8n в Docker с volume для сохранения данных;
- строить визуальные workflow, соединяя ноды;
- писать JS-код в ноде Code и использовать `let/const`, `if/else`, циклы;
- работать с публичными API через HTTP Request;
- настраивать расписание через Schedule Trigger;
- работать с Redis: Set/Get/Delete ключей;
- реализовывать **Pub/Sub** между двумя независимыми workflow (ачивка №10).

Самым интересным было увидеть, как два независимых workflow могут общаться через **Redis Pub/Sub** — Publisher отправляет сообщение в канал, а Subscriber ловит его в реальном времени. Это основа для асинхронных систем и микросервисной архитектуры.

По сравнению с Node-RED, n8n показался более «программистским» — больше внимания к данным, но в целом похожий подход. Оба инструмента — мощные low-code платформы, но с разными акцентами.