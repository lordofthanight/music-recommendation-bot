# Чат-бот рекомендаций музыки (FastAPI + Spotify)

Бот рекомендует треки из Spotify по настроению и жанру (например: "рекомендуй энергичное rock").

## Функционал
- Регистрация и логин с JWT-токеном
- Создание сессий чата
- WebSocket-чат в реальном времени (альтернатива POST /chat/message)
- Рекомендации из Spotify API
- Сохранение истории диалога (пользователь + бот)
- Защищённый доступ (проверка JWT и принадлежности сессии)
- Swagger UI для документации

## Технологии
- FastAPI
- SQLAlchemy (async)
- Alembic (миграции)
- Pydantic (валидация)
- JWT + bcrypt (аутентификация)
- spotipy (Spotify API)
- WebSocket
- pytest (тесты)

## Структура проекта

├── app/
│   ├── main.py            # точка входа
│   ├── config.py          # настройки из .env
│   ├── database.py        # подключение к БД
│   ├── models.py          # модели SQLAlchemy
│   ├── schemas.py         # Pydantic-схемы
│   ├── crud.py            # операции с БД
│   ├── auth.py            # JWT, хэширование
│   ├── spotify_client.py  # клиент Spotify
│   ├── bot_logic.py       # логика бота
│   └── routers/
│       ├── auth.py        # /auth/register, /auth/login
│       └── chat.py        # сессии, история, WebSocket
├── migrations/            # Alembic миграции
├── tests/                 # автоматизированные тесты
├── .env.example           # пример настроек
├── alembic.ini
├── requirements.txt
└── README.md


## Запуск

1. Клонируйте репозиторий
2. Создайте виртуальное окружение:
   ```bash
   cd путь-до-бота/Documents/bot
   python -m venv venv
   source venv313/bin/activate  # macOS/Linux
   # или venv\Scripts\activate  # Windows

3. Установите зависимости: pip install -r requirements.txt
4. Создайте .env из .env.example и заполните:
    SECRET_KEY (случайная строка)
    SPOTIFY_CLIENT_ID и SPOTIFY_CLIENT_SECRET (из https://developer.spotify.com/dashboard)

5. Примените миграции: alembic upgrade head
6. Запустите сервер: uvicorn app.main:app --reload
7. Откройте в браузере: http://127.0.0.1:8000/docs (Swagger UI)

## Использование

Зарегистрируйтесь (/auth/register) → получите токен
Создайте сессию (/chat/session, токен в query)
Подключитесь к WebSocket: ws://127.0.0.1:8000/chat/ws?token=ваш_токен
Отправьте {"text": "рекомендуй энергичное pop"}
Получите ответ