# Taski 📝

## Описание
**Taski** — это REST API сервис для управления задачами (To-Do List). Проект предоставляет удобный интерфейс для создания, чтения, редактирования и удаления задач.

**Ключевые особенности и логика API:**
* **CRUD операции:** Полный набор эндпоинтов для управления задачами.
* **Кастомное удаление:** При удалении задачи эндпоинт возвращает данные удаленного объекта (со статусом `200 OK`), а не пустой ответ (`204 No Content`).
* **Статус выполнения:** Задачи по умолчанию создаются со статусом "не выполнено" (`completed: false`).

---

## Установка (Локальный запуск)
Инструкция по развертыванию проекта на локальной машине для разработки и тестирования.

1. **Клонируйте репозиторий:**
   ```bash
   git clone git@github.com:Bobrovskii13/taski-docker.git
   cd taski-docker/backend
   ```

2. **Создайте и активируйте виртуальное окружение:**
   
   *Для Windows:*
   ```bash
   py -3.12 -m venv venv
   source venv/Scripts/activate
   ```
   
   *Для Linux/macOS:*
   ```bash
   py -3.12 -m venv venv
   source venv/bin/activate
   ```

3. **Установите зависимости:**
   ```bash
   pip install -r requirements.txt
   ```

4. **Примените миграции:**
   ```bash
   python manage.py makemigrations
   python manage.py migrate
   ```

5. **Запустите локальный сервер:**
   ```bash
   python manage.py runserver
   ```
   После запуска API будет доступно по адресу: `http://127.0.0.1:8000/api/`

---

## Примеры запросов к API

### 1. Получение списка всех задач

**Запрос:** `GET /api/tasks/`
 
**Ответ (200 OK):**
```json
[
  {
    "id": 1,
    "title": "Купить молоко",
    "description": "Зайти в магазин после работы",
    "completed": false
  },
  {
    "id": 2,
    "title": "Написать README",
    "description": "Добавить описание для проекта Taski",
    "completed": true
  }
]
```

### 2. Создание новой задачи
 
**Запрос:** `POST /api/tasks/`
 
**Заголовки:**  
`Content-Type: application/json`
 
**Тело запроса (JSON):**
```json
{
  "title": "Изучить Docker",
  "description": "Пройти туториал по контейнеризации приложений"
}
```
**Ответ (201 Created):**
```json
{
  "id": 3,
  "title": "Изучить Docker",
  "description": "Пройти туториал по контейнеризации приложений",
  "completed": false
}
```

### 3. Частичное обновление задачи (отметка о выполнении)

**Запрос:** `PATCH /api/tasks/3/`
 
**Заголовки:**  
`Content-Type: application/json`
 
**Тело запроса (JSON):**
```json
{
  "completed": true
}
```
**Ответ (200 OK):**
```json
{
  "id": 3,
  "title": "Изучить Docker",
  "description": "Пройти туториал по контейнеризации приложений",
  "completed": true
}
```

### 4. Удаление задачи

> **Примечание:** В отличие от стандартного поведения DRF, API Taski при удалении возвращает JSON с данными удаленной задачи и статусом `200 OK`.

**Запрос:** `DELETE /api/tasks/3/`
 
**Ответ (200 OK):**
```json
{
  "id": 3,
  "title": "Изучить Docker",
  "description": "Пройти туториал по контейнеризации приложений",
  "completed": true
}
```

[![Main Taski workflow](https://github.com/Bobrovskii13/taski-docker/actions/workflows/main.yml/badge.svg?branch=main)](https://github.com/Bobrovskii13/taski-docker/actions/workflows/main.yml)
