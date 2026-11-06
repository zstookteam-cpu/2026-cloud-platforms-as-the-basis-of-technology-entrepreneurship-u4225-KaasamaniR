University: [ITMO University](https://itmo.ru/ru/)
Faculty: [FICT](https://fict.itmo.ru)
Course: [Cloud platforms as the basis of technology entrepreneurship](https://github.com/itmo-ict-faculty/cloud-platforms-as-the-basis-of-technology-entrepreneurship)
Year: 2026/2027
Group: U4225
Author: Kaasamani Roni Bahaaevich
Lab: Lab2
Date of create: 03.11.2026
Date of finished: ДД.ММ.ГГГГ (дата защиты)

# Лабораторная работа №2. Исследование Cloud Run

## Цель работы

Ознакомиться с принципами работы Cloud Run.

## Ход работы

### 1. Создание сервиса

Cloud Run → Create service. Вариант: стандартный «Hello» (или собственный контейнер — предпочтительнее). Минимальные ресурсы: 1 vCPU / 128–512 MiB, min instances = 0, max instances = 1.

> 📸 `img/01_create_service.png` — форма создания сервиса.
> 📸 `img/02_service_ready.png` — сервис создан, виден URL.

### 2. Проверка по URL

> 📸 `img/03_service_url.png` — страница сервиса в браузере.

### 3. Логи и метрики

Вкладки Logs и Metrics: запросы, задержка, число инстансов, холодный старт.

> 📸 `img/04_logs.png`
> 📸 `img/05_metrics.png`

Наблюдения: *(заполнить)*

### 4. Смена порта на 8090

Edit & deploy new revision → Container port = 8090. Ожидаемо: контейнер слушает другой порт, ревизия не проходит startup-проверку и не становится Ready.

> 📸 `img/06_port_8090.png` — настройка порта.
> 📸 `img/07_port_result.png` — результат (ошибка/статус ревизии).
> 📸 `img/08_port_logs.png` — логи с причиной.

Наблюдения: *(заполнить по факту)*

### 5. Распределение трафика между ревизиями

Tab Revisions → Manage traffic (например, 50/50 или 80/20 между рабочей и новой ревизией).

> 📸 `img/09_traffic_split.png`
> 📸 `img/10_traffic_compare.png` — сравнение ответов/метрик.

### 6. Удаление ресурсов

> 📸 `img/11_cleanup.png` — список сервисов пуст.

## Выводы

*(Заполнить: модель serverless, scale-to-zero, ревизии, canary-раскатка, роль PORT.)*
