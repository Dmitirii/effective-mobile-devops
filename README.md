# 🚀 Effective Mobile – Тестовое задание DevOps

Простое веб-приложение, развёрнутое в Docker-контейнерах с reverse proxy на Nginx.

![Docker](https://img.shields.io/badge/docker-%230db7ed.svg?style=for-the-badge&logo=docker&logoColor=white)
![Docker Compose](https://img.shields.io/badge/docker_compose-%232496ED.svg?style=for-the-badge&logo=docker&logoColor=white)
![Python](https://img.shields.io/badge/python-3.11-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54)
![Nginx](https://img.shields.io/badge/nginx-%23009639.svg?style=for-the-badge&logo=nginx&logoColor=white)
![Alpine](https://img.shields.io/badge/alpine-%230d597f.svg?style=for-the-badge&logo=alpine-linux&logoColor=white)

## 📋 Содержание
- [Как запустить проект](#как-запустить-проект)
- [Как проверить результат](#как-проверить-результат)
- [Архитектура](#архитектура)
- [Структура проекта](#структура-проекта)
- [Команды Docker Compose](#команды-docker-compose)
- [Безопасность и рекомендации](#безопасность-и-рекомендации)

---

## 🚀 Как запустить проект

### Предварительные требования
- [Docker](https://docs.docker.com/engine/install/) и [Docker Compose](https://docs.docker.com/compose/install/)
- Git (для клонирования)

### Установка и запуск
```bash
git clone https://github.com/Dmitirii/effective-mobile-devops.git
cd effective-mobile-devops
docker compose up -d
