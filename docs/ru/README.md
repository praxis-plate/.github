# Платформа Praxis

[![Dart](https://img.shields.io/badge/Dart-3.10-blue.svg)](https://dart.dev)
[![Flutter](https://img.shields.io/badge/Flutter-3.38-blue.svg)](https://flutter.dev)
[![Serverpod](https://img.shields.io/badge/Serverpod-2.x-orange.svg)](https://serverpod.dev)

Образовательная платформа для интерактивных курсов программирования с AI-ассистентом и отслеживанием прогресса.

**[Быстрый старт](#быстрый-старт)** • **[Архитектура](#архитектура)** • **[Разработка](#разработка)**

---

**Языки:** [English](../../README.md) • [Русский](#)

## Обзор

Praxis – это full-stack образовательная платформа, состоящая из:

- **[praxis-flutter](https://github.com/praxis-plate/praxis-flutter)** – кроссплатформенное мобильное/веб-приложение (Flutter)
- **[praxis-api](https://github.com/praxis-plate/praxis-api)** – backend API-сервер (Serverpod/Dart)

### Основные возможности

- **Интерактивное обучение** – курсы, модули, уроки с различными типами заданий (множественный выбор, дополнение кода, сопоставление, текстовый ввод)
- **Отслеживание прогресса** – завершение уроков, статистика, достижения, ежедневные серии
- **Виртуальный кошелёк** – внутренняя система монет и наград (без интеграции с реальными деньгами)
- **AI-ассистент** – генерация подсказок и объяснений через интеграцию с LLM (опционально)
- **Аутентификация** – провайдер идентификации на основе email с JWT-токенами

## Архитектура

Платформа следует **клиент-серверной архитектуре** с чётким разделением:

![Обзор архитектуры](../../diagrams/images/architecture-overview.png)

*[Посмотреть UML-исходник](../../diagrams/uml/architecture-overview.puml)*

### Технологический стек

- **Frontend:** Flutter 3.38, паттерн BLoC, Clean Architecture
- **Backend:** Serverpod 2.x, Dart 3.10
- **Коммуникация:** RPC (Remote Procedure Call) через сгенерированный Serverpod-клиент
- **База данных:** PostgreSQL (с pgvector)
- **Кэш/Сессии:** Redis
- **AI-интеграция:** Google Gemini API (опционально)

**Примечание:** Serverpod-клиент автоматически генерируется из определений протокола сервера, обеспечивая типобезопасные RPC-вызовы между клиентом и сервером.

## Быстрый старт

### Требования

- [FVM](https://fvm.app) (Flutter Version Management)
- [Docker Desktop](https://www.docker.com/products/docker-desktop)
- Dart 3.10+ / Flutter 3.38+ (управляется через FVM)

### 1. Клонировать репозиторий

```bash
git clone <repository-url>
cd praxis
```

### 2. Запустить Backend

```bash
cd praxis-api

# Запустить Postgres + Redis
docker compose up --build --detach

# Установить зависимости
fvm dart pub get

# Настроить секреты (отредактировать config/passwords.yaml)
# См. README репозитория для деталей

# Запустить сервер
fvm dart run bin/main.dart
```

Сервер запустится на `http://localhost:8080`

### 3. Запустить Frontend

```bash
cd praxis_flutter

# Установить зависимости
fvm flutter pub get

# Настроить окружение (отредактировать .env)
# См. praxis_flutter/README.md для деталей

# Запустить приложение
fvm flutter run
```

## Структура проекта

```
praxis/
├── .github/              # Документация платформы
├── praxis_flutter/       # Flutter мобильное/веб-приложение
│   ├── lib/
│   │   ├── features/     # UI-функции (auth, courses, lessons, tasks)
│   │   ├── domain/       # Бизнес-логика (models, repositories, use cases)
│   │   ├── data/         # Слой данных (entities, data sources, repositories)
│   │   └── core/         # Общие утилиты (theme, routing, config)
│   └── README.md
├── praxis-api/           # Serverpod backend
│   ├── lib/src/
│   │   ├── endpoints/    # API-эндпоинты
│   │   ├── usecases/     # Оркестрация бизнес-логики
│   │   ├── services/     # Доменные сервисы
│   │   ├── datasources/  # Доступ к базе данных
│   │   └── models/       # Модели протокола
│   ├── config/           # Конфигурации окружений
│   ├── migrations/       # Миграции базы данных
│   └── README.md
├── AGENTS.md             # Рекомендации для AI-ассистентов
```

## Разработка

### Использование FVM

Этот workspace использует FVM для управления версиями Dart/Flutter SDK. Всегда используйте команды FVM:

```bash
# Проверить версии
fvm dart --version
fvm flutter --version

# Установить зависимости
fvm dart pub get      # для praxis-api
fvm flutter pub get   # для praxis_flutter
```

### Соглашение о коммитах

Используйте сообщения коммитов с тикетами:

```
[TICKET-ID] Краткое описание на русском или английском

Примеры:
[PA-14] Добавил эндпоинт для получения lesson по id
[CDM-23] Поправил детальную страницу
```

Для подробных рекомендаций по разработке, генерации кода, тестированию и развертыванию см.:
- [praxis-api](https://github.com/praxis-plate/praxis-api) – разработка backend
- [praxis-flutter](https://github.com/praxis-plate/praxis-flutter) – разработка frontend
- [AGENTS.md](../AGENTS.md) – рекомендации для AI-ассистентов

## Документация

Для получения подробной информации о каждом компоненте см. соответствующую документацию:

- **Backend:** [praxis-api](https://github.com/praxis-plate/praxis-api)
- **Frontend:** [praxis-flutter](https://github.com/praxis-plate/praxis-flutter)
- **Рекомендации для AI:** [AGENTS.md](../AGENTS.md)

### Внешние ресурсы

- [Документация Serverpod](https://docs.serverpod.dev)
- [Документация Flutter](https://docs.flutter.dev)
- [Effective Dart](https://dart.dev/guides/language/effective-dart)

## Лицензия

Это образовательный проект, разработанный для университетских целей.
