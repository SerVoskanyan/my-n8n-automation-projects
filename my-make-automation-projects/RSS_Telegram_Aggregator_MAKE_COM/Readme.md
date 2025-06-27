# 🇦🇲 RSS Агрегатор Новостей Армении для Telegram_Author Serik_Voskanyan

## 📝 Описание Проекта

Этот проект представляет собой сценарий Make.com (ранее Integromat), разработанный для автоматической агрегации новостей из нескольких армянских RSS-лент и их последующей публикации в указанный Telegram-канал. Целью является централизованное получение и распространение новостной информации из ключевых армянских медиаисточников.

### 🌐 Используемые Источники RSS:

* **Sputnik Армения (arm.sputniknews.ru)** - Основной триггер сценария.
* **1lurer.am** - Получение новостей по запросу.
* **News.am** - Получение новостей по запросу.
* **Armradio.am** - Получение новостей по запросу.

## ⚙️ Схема Сценария Make.com

```mermaid
graph TD
    A[RSS (Sputnik) - Watch RSS feed items] --> B(Set Multiple Variables)
    B --> C{Router}

    C --> D1(RSS (Retrieve RSS feed items) - News.am)
    D1 --> F1{Filter: Только News.am}
    F1 --> G1(Telegram Bot - Send Text Message)

    C --> D2(RSS (Retrieve RSS feed items) - 1lurer.am)
    D2 --> F2{Filter: Только 1lurer.am}
    F2 --> G2(Telegram Bot - Send Text Message)

    C --> D3(RSS (Retrieve RSS feed items) - Armradio.am)
    D3 --> F3{Filter: Только Armradio.am}
    F3 --> G3(Telegram Bot - Send Text Message)

    C --> D4(Telegram Bot - Send Text Message)
    D4 --> F4{Filter: Только Sputnik}
    F4 --> G4(Telegram Bot - Send Text Message)
    
   