Effective Mobile – тестовое задание DevOps

Веб-приложение с обратным прокси-сервером nginx, развёрнутое в Docker-контейнерах.

ТРЕБОВАНИЯ

- Docker Engine версии 20.10 или выше
- Плагин Docker Compose v2 (команда docker compose)
- Git для клонирования репозитория

СТРУКТУРА ПРОЕКТА

effective-mobile-devops/
    backend/
        Dockerfile
        app.py
    nginx/
        nginx.conf
    docker-compose.yml
    .env (локальный, не включён в Git)
    .gitignore
    README.md

ЗАПУСК ПРОЕКТА

1. Клонировать репозиторий:
   git clone https://github.com/Dmitirii/effective-mobile-devops.git

2. Перейти в директорию проекта:
   cd effective-mobile-devops

3. Создать файл .env (требуется для настройки порта nginx):
   echo "NGINX_PORT=80" > .env

4. Запустить сервисы в фоновом режиме:
   docker compose up -d

После запуска веб-приложение доступно на порту 80.

ПРОВЕРКА РАБОТОСПОСОБНОСТИ

Выполнить HTTP-запрос:
   curl http://localhost

Ожидаемый ответ:
   Hello from Effective Mobile!

Тот же результат можно получить, открыв в браузере http://localhost.

АРХИТЕКТУРА

Схема взаимодействия:
[Пользователь] → (порт 80) → [nginx] → (порт 8080, внутренняя сеть app-net) → [backend]

Компоненты:

- Backend
  Python HTTP-сервер (http.server).
  Слушает порт 8080 внутри Docker-сети app-net.
  Прямой доступ с хоста отсутствует (порт не проброшен).

- Nginx
  Официальный образ nginx:stable-alpine.
  Принимает HTTP-запросы на порт 80.
  Проксирует запросы на backend по имени сервиса (proxy_pass http://backend;).
  Конфигурация монтируется как том в режиме read-only.

- Сеть
  Изолированная bridge-сеть app-net.
  Сервисы взаимодействуют друг с другом по именам, заданным в docker-compose.yml.

- Переменные окружения
  Порт, на котором nginx принимает соединения, определяется переменной NGINX_PORT
  из файла .env (по умолчанию 80).

КОМАНДЫ УПРАВЛЕНИЯ

docker compose up -d      Запуск сервисов в фоновом режиме
docker compose down       Остановка и удаление контейнеров
docker compose ps         Просмотр состояния контейнеров
docker compose config     Проверка итоговой конфигурации с учётом .env

БЕЗОПАСНОСТЬ И РЕКОМЕНДАЦИИ

- Backend-контейнер запускается от непривилегированного пользователя nobody.
- Используются легковесные alpine-образы для уменьшения размера и поверхности атаки.
- Наружу проброшен только порт 80 (nginx), порт backend скрыт внутри сети.
- Конфигурация Nginx монтируется в режиме read-only (:ro).
- Файл .env исключён из Git через .gitignore – секреты и локальные настройки не попадают в репозиторий.
- При проксировании передаются заголовки Host, X-Real-IP, X-Forwarded-For.
- Для сетевого взаимодействия не используются захардкоженные IP-адреса.

ИСПОЛЬЗОВАННЫЕ ТЕХНОЛОГИИ

Docker, Docker Compose – контейнеризация и оркестрация
Python 3.11 (alpine) – backend-сервер
Nginx (stable-alpine) – обратный прокси-сервер
Alpine Linux – базовый образ для минимизации размера
