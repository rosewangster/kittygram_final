# Kittygram

Социальная сеть для любителей котиков. Пользователи могут регистрироваться, загружать фотографии своих котов с именем и годом рождения, а также просматривать котиков других пользователей.

## Стек технологий

- **Backend:** Python, Django, Django REST Framework
- **Frontend:** React
- **База данных:** PostgreSQL
- **Веб-сервер:** Nginx
- **Контейнеризация:** Docker, Docker Compose
- **CI/CD:** GitHub Actions

## Как развернуть проект локально

### 1. Клонировать репозиторий

```bash
git clone git@github.com:rosewangster/kittygram_final.git
cd kittygram_final
```

### 2. Создать файл `.env`

Скопировать пример и заполнить своими значениями:

```bash
cp .env.example .env
```

Открыть `.env` и заполнить переменные:

```dotenv
SECRET_KEY=придумайте-любой-длинный-секретный-ключ
DEBUG=False
ALLOWED_HOSTS=localhost 127.0.0.1

POSTGRES_DB=kittygram
POSTGRES_USER=kittygram_user
POSTGRES_PASSWORD=придумайте-пароль
POSTGRES_HOST=db
POSTGRES_PORT=5432
```

### 3. Запустить контейнеры

```bash
docker compose up --build
```

### 4. Выполнить миграции

```bash
docker compose exec backend python manage.py migrate
```

### 5. Открыть проект

Перейти в браузере на `http://localhost:9000`

## Описание переменных окружения

| Переменная | Описание |
|-----------|----------|
| `SECRET_KEY` | Секретный ключ Django, должен быть длинным и уникальным |
| `DEBUG` | Режим отладки. В production всегда `False` |
| `ALLOWED_HOSTS` | Разрешённые хосты, перечисляются через пробел |
| `POSTGRES_DB` | Название базы данных |
| `POSTGRES_USER` | Пользователь базы данных |
| `POSTGRES_PASSWORD` | Пароль пользователя базы данных |
| `POSTGRES_HOST` | Хост базы данных (в Docker — имя сервиса `db`) |
| `POSTGRES_PORT` | Порт базы данных, по умолчанию `5432` |

## CI/CD

При пуше в ветку `main` автоматически запускается GitHub Actions workflow, который:

1. Проверяет код бэкенда линтером `ruff`
2. Запускает тесты бэкенда и фронтенда
3. Собирает Docker-образы и загружает их на Docker Hub
4. Отправляет уведомление в Telegram об успешном завершении

Образы на Docker Hub:
- `kazinakdi/kittygram_backend`
- `kazinakdi/kittygram_frontend`
- `kazinakdi/kittygram_gateway`
