# n8n-yandex-email-to-googlesheet
Автоматизация n8n: Запись новых писем из Яндекс Почты в Google Таблицы

# Автоматизация n8n: Запись новых писем из Яндекс Почты в Google Таблицы

## 💡 Обзор Проекта

Этот проект демонстрирует, как использовать n8n для автоматической обработки новых входящих писем из Яндекс Почты и записи ключевой информации (Отправитель, Тема, Дата Получения, Очищенное Сообщение) в Google Таблицы. Это позволяет эффективно вести учет корреспонденции или создавать базу данных писем без ручного ввода.

## ✨ Основные Функции

* Получение новых писем из Яндекс Почты (через IMAP).
* Извлечение и структурирование данных письма: отправитель, тема, дата/время получения.
* **Форматирование даты и времени** в удобный для чтения формат (например, "04 июня 2025 15:30").
* **Очистка тела письма** от HTML-тегов, URL-адресов и лишних символов, оставляя только чистый текст.
* Автоматическая запись обработанных данных в указанную Google Таблицу.

## 🛠️ Используемые Технологии

* **n8n:** Open-source инструмент для автоматизации workflow.
* **Яндекс Почта:** Источник входящих писем.
* **Google Sheets:** Целевая таблица для сохранения данных.
* **JavaScript:** Для кастомной обработки данных в узле "Code".

## 🚀 Как Запустить / Использовать

1.  **Установите и запустите n8n:** Вы можете использовать локальную установку, Docker или облачный сервис n8n.
2.  **Импортируйте Workflow:**
    * Скачайте файл `Yandex_Mail_to_Google_Sheets ` (мы его экспортируем позже).
    * В интерфейсе n8n, нажмите "New Workflow" -> "Import from JSON".
    * Вставьте содержимое файла или загрузите его.
3.  **Настройте Подключения (Credentials):**
    * **Яндекс Почта (IMAP):** В узле "Email Trigger" убедитесь, что ваше IMAP-подключение к Яндекс Почте настроено и активно.
    * **Google Sheets:** В узле "Google Sheets" настройте подключение к вашему Google аккаунту и укажите ID таблицы, а также имя листа, куда будут записываться данные.
4.  **Активируйте Workflow:** Нажмите кнопку "Activate" в правом верхнем углу n8n.

## 📁 Структура Workflow

Workflow состоит из следующих узлов:

1.  **Email Trigger (IMAP):** Запускает workflow при получении нового письма.
    * *Настройки:* Подключение к Яндекс Почте через IMAP.
2.  **Set:** Извлекает и переименовывает ключевые поля письма:
    * `Отправитель` (из `email.from.name`)
    * `Тема` (из `email.subject`)
    * `Дата Получения` (из `email.receivedDate`)
    * `Сообщение` (из `email.text`)
3.  **Code:** Обрабатывает и форматирует данные:
    * Форматирует `Дата Получения` в `ФорматированнаяДата` (например, "04 июня 2025 15:30").
    * Очищает `Сообщение` от HTML-тегов, URL-адресов и лишних пробелов, сохраняя в `ОчищенноеСообщение`.
4.  **Google Sheets:** Записывает обработанные данные в новую строку Google Таблицы.
    * *Настройки:* ID Таблицы, Имя Листа, маппинг полей (`Отправитель`, `Тема`, `ФорматированнаяДата`, `ОчищенноеСообщение`).

## ✍️ Автор

[Serik]
[https://www.linkedin.com/in/sergey-voskanyan/]

## 📄 Лицензия

Этот проект распространяется под лицензией MIT.
