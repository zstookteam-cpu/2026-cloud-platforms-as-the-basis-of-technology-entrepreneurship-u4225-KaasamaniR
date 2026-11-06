University: [ITMO University](https://itmo.ru/ru/)
Faculty: [FICT](https://fict.itmo.ru)
Course: [Cloud platforms as the basis of technology entrepreneurship](https://github.com/itmo-ict-faculty/cloud-platforms-as-the-basis-of-technology-entrepreneurship)
Year: 2026/2027
Group: U4225
Author: Kaasamani Roni Bahaaevich
Lab: Lab3
Date of create: 03.11.2026
Date of finished: ДД.ММ.ГГГГ (дата защиты)

# Лабораторная работа №3. Исследование Cloud Storage

## Цель работы

Ознакомиться с основными понятиями и принципами работы облачного хранилища: блочное, файловое и объектное хранение, сервисы и функции облачных хранилищ.

## Теоретическая часть (кратко)

*(Сравнительная таблица: блочное / файловое / объектное — примеры в Google Cloud: Persistent Disk, Filestore, Cloud Storage; классы хранения Standard / Nearline / Coldline / Archive.)*

## Ход работы

### 1. Проект

> 📸 `img/01_project.png`

### 2. Создание bucket

Уникальное имя, регион, класс хранения Standard.

> 📸 `img/02_bucket_create.png`
> 📸 `img/03_bucket_created.png`

### 3. Загрузка 3–4 изображений

> 📸 `img/04_upload.png`

### 4. Папка и перемещение файлов

> 📸 `img/05_folder.png`

### 5. Публичный доступ

Permissions → Grant access → principal `allUsers`, роль `Storage Object Viewer` (при необходимости отключить Public access prevention).

> 📸 `img/06_public_access.png`

### 6. Ссылка на файл

Контекстное меню файла → Copy public URL. Проверка открытия в режиме инкогнито.

> 📸 `img/07_public_url.png`
> 📸 `img/08_incognito_open.png`

### 7. Удаление ресурсов

> 📸 `img/09_cleanup.png`

## Выводы

*(Заполнить.)*
