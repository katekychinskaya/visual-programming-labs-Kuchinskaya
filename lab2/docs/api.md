# Node-RED REST API — лабораторная 2.8

## Общая информация

- Базовый URL: `http://localhost:1880`
- Формат ответа: JSON для `/api/info` и `/api/items`, plain text для `/api/text`

## Эндпоинты

### 1. GET /api/text

Возвращает простой текст.

**Пример запроса:**
```
GET http://localhost:1880/api/text
```

**Пример ответа (200 OK):**
```
Привет! Это текстовый ответ от Node-RED. Студент: Кучинская.
```

### 2. GET /api/info

Возвращает JSON-объект с информацией о студенте.

**Пример запроса:**
```
GET http://localhost:1880/api/info
```

**Пример ответа (200 OK):**
```json
{
    "student": "Кучинская",
    "lab": "lab2",
    "task": "2.8 endpoints"
}
```

### 3. GET /api/items/:id

Возвращает товар по его id.

**Параметры пути:**
- `id` (обязательный) — идентификатор товара (1, 2, 3)

**Успешный запрос:**
```
GET http://localhost:1880/api/items/1
```

**Успешный ответ (200 OK):**
```json
{
    "success": true,
    "item": {
        "name": "Пицца",
        "price": 15
    }
}
```

**Запрос с несуществующим id:**
```
GET http://localhost:1880/api/items/999
```

**Ответ с ошибкой (404 Not Found):**
```json
{
    "success": false,
    "error": "Товар с id=999 не найден"
}
```

## Коды ответов

| Код | Когда возвращается |
|-----|-------------------|
| 200 | Успешный запрос |
| 404 | Товар с указанным id не найден |

## Список товаров (для проверки)

| id | name | price |
|----|------|-------|
| 1 | Пицца | 15 |
| 2 | Суши | 25 |
| 3 | Бургер | 10 |

## Скриншоты

- `screenshots/08a-2.8-text.png` — ответ /api/text
- `screenshots/08b-2.8-info.png` — ответ /api/info
- `screenshots/08c-2.8-items-ok.png` — успешный /api/items/1
- `screenshots/08d-2.8-items-404.png` — ошибочный /api/items/999
- `screenshots/08-2.8-flow.png` — холст Node-RED