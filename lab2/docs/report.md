# Отчёт по лабораторной работе №2. Node-RED

**Студент:** Кучинская Екатерина  
**Тема:** Освоение Node-RED как low-code инструмента

---

## 1. Краткое описание выполненного

В ходе лабораторной работы я установила Node-RED в Docker-контейнере и освоила его как визуальный low-code инструмент для построения потоков обработки данных. Были собраны и задеплоены **12 различных flow**, охватывающих базовые и расширенные ноды, а также выполнена **ачивка №3 (JWT-аутентификация)**.

Все flow сохранены в папке `lab2/flows/` в виде отдельных JSON-файлов, скриншоты — в `lab2/screenshots/`, документация API — в `lab2/docs/api.md`.

---

## 2. Способ установки и версии

- **Способ установки:** Docker (образ `nodered/node-red`)
- **Команда запуска:** docker run -it -p 1880:1880 -v node_red_data:/data --name mynodered nodered/node-red
- **Node-RED version:** v5.0.7
- **Node.js version:** v24.20.0
- **ОС:** Windows 11 Pro, WSL2

---

## 3. Освоенные ноды

| Нода | Что освоила |
|---|---|
| `inject` | Запуск потока, интервалы, payload разных типов |
| `debug` | Просмотр сообщений, complete msg object |
| `function` | JS-код: let/const, if/else, for, массивы, объекты |
| `switch` | Ветвление по правилам (`==`, свойства msg) |
| `change` | Установка/изменение полей msg (payload, topic, timestamp) |
| `template` | Mustache-шаблоны, генерация JSON |
| `http request` | GET-запросы к публичным API, parsed JSON |
| `mqtt in` / `mqtt out` | Публикация и подписка на публичном брокере HiveMQ |
| `http in` / `http response` | Создание REST-эндпоинтов |
| `dashboard: gauge, chart` | Визуализация данных на веб-панели |
| `telegram receiver/sender/command` | Создание Telegram-бота с командами |
| `file in` / `file out` | Чтение и запись файлов в volume |
| `flow context` | Счётчик, живущий между сообщениями |
| `http in POST` + function | JWT-аутентификация |

---

## 4. Ключевые AI-промпты

- «Сгенерируй JS-код для Node-RED function node: используй let/const, if/else, цикл for, массив и объект. Функция должна возвращать объект с полем payload»
- «Объясни, как в Node-RED настроить switch для ветвления по msg.payload.category на значения "большое" и "маленькое"»
- «Сгенерируй Mustache-шаблон для template node, который формирует JSON из полей msg.payload»
- «Напиши код function node для JWT-токена: создание и проверка подписи HMAC-SHA256, проверка срока действия»
- «Почему require не работает в Node-RED function node и как обойти?»

---

## 5. Скриншоты flow

Все скриншоты находятся в `lab2/screenshots/`:

| Файл | Что на нём |
|---|---|
| `01.1-versions.png` | Версии Node-RED |
| `01.2-versions.png` | Версии Node.js |
| `02-inject-debug.png` | Первый flow inject → debug |
| `03-2.1-inject-debug.png` | 2.1 — Inject с фамилией и topic |
| `04-2.2-function.png` | 2.2 — Function node |
| `05-2.3-switch.png` | 2.3 — Switch с двумя выходами |
| `06-2.4-change.png` | 2.4 — Change node |
| `07-2.5-template.png` | 2.5 — Template Mustache |
| `08-2.6-http-request.png` | 2.6 — HTTP Request к Chuck Norris API |
| `09-2.7-mqtt.png` | 2.7 — MQTT publish/subscribe |
| `08a-2.8-text.png` … `08d-2.8-items-404.png` | 2.8 — GET-эндпоинты |
| `10-2.9-dashboard.png` | 2.9 — Dashboard с gauge и chart |
| `11-2.10-telegram.png` | 2.10 — Telegram-бот |
| `11c-botfather.png` | Скриншот BotFather |
| `12-2.11-files-flow.png` | 2.11 — Работа с файлами |
| `12b-2.11-files-after-restart.png` | 2.11 — Данные после перезапуска |
| `13-2.12-context-flow.png` | 2.12 — Контекст (счётчик) |
| `14b-achiev3-me.png` | Ачивка 3 — успешный JWT-логин |
| `14c-achiev3-tests.png` | Ачивка 3 — все тесты |

---

## 6. Выводы

В ходе лабораторной работы я научилась:
- устанавливать и запускать Node-RED в Docker с сохранением данных через volume;
- строить визуальные потоки обработки данных, соединяя ноды;
- писать JS-код в function-нодах и использовать flow context;
- работать с публичными API (HTTP, MQTT);
- создавать собственные REST-эндпоинты и документировать их;
- визуализировать данные через dashboard;
- делать Telegram-бота с командами;
- реализовывать JWT-аутентификацию без внешних библиотек;
- работать с файлами и контекстом между перезапусками.

Самым сложным было разобраться с ограничениями function-нод (запрет `require`) и настройкой Dashboard (правильная конфигурация групп и вкладок). Node-RED показался очень удобным инструментом для быстрого прототипирования — за пару часов можно собрать рабочий backend с API, ботом и визуализацией.