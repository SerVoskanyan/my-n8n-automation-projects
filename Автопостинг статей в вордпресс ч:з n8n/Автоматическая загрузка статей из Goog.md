# Автоматическая загрузка статей из Google Sheets на сайт WordPress (тема The7) через n8n

## 1. Источник данных — Google Sheets
### 1.1 Подготовка таблицы
- Заголовок статьи (title)
- Основной текст (content)
- Краткое описание (excerpt / description)
- Название для генерации картинки
- Категория / теги
- Статус: "draft" или "publish"
- Флаг "опубликовано" (да/нет)
- Столбец для обратной связи (ссылка на статью / ошибка)

### 1.2 Подключение Google Sheets к n8n
- Node: Google Sheets (credentials уже подключены)
- Read Rows из таблицы
- Фильтр: "опубликовано" = нет
- Cron Trigger или Manual Trigger

## 2. Генерация изображения (автоматически)
### 2.1 Генерация в n8n
- Node: HTTP Request (к OpenRouter, DALL·E или Hugging Face)
- Передать описание из таблицы
- Получить URL сгенерированного изображения

### 2.2 Обработка изображения
- Node: HTTP Request → download image
- Node: Set / Binary → подготовка к загрузке
- Node: Move Binary Data → подготовить multipart

## 3. Публикация в WordPress через REST API
### 3.1 Подключение в n8n
- Node: HTTP Request
- Аутентификация: JWT (используется полученный токен)
- URL: `https://site.ru/wp-json/wp/v2/...`

### 3.2 Загрузка изображения
- Node: HTTP Request → `POST /media`
- Заголовки: Content-Type, Authorization, filename
- Тело: изображение
- Получить `featured_media ID`

### 3.3 Создание поста
- Node: HTTP Request → `POST /posts`
- Включить:
    - `title`
    - `content`
    - `status`
    - `featured_media` (ID)
    - `categories`, `tags` (если заданы)

## 4. Обратная связь и логика
### 4.1 Обновление Google Sheets в n8n
- Node: Google Sheets → Update Row
- Поставить "опубликовано" = да
- Вставить ссылку на пост
- В случае ошибки → записать в отдельную колонку

### 4.2 Уведомления
- Node: Telegram (если подключён)
- Node: Email (SMTP / Gmail)
- Уведомить об успешной публикации или ошибке

## 5. SEO оптимизация (опционально)
### 5.1 Генерация мета‑описания
- Node: Function или AI Agent (GPT)
- Сгенерировать description из текста статьи

### 5.2 Интеграция с SEO-плагином WordPress (если нужно)
- Node: HTTP Request → RankMath или AIOSEO API (если есть)
- Обновление мета-заголовков и Open Graph

## 6. Управление процессом
### 6.1 Глобальный контроль в n8n
- Node: IF — логика фильтрации
- Node: Error Handling — перехват ошибок
- Node: Wait или Delay (если API ограничено)
- Использовать Sub-workflow при необходимости
