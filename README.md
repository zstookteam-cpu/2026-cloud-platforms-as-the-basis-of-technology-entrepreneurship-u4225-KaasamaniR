# Облачные платформы как основа технологического предпринимательства

Репозиторий с отчётами по лабораторным работам курса «Облачные платформы как основа технологического предпринимательства».

- **Университет:** ИТМО
- **Студент:** Каасамани Рони Бахааевич
- **Группа:** U4225
- **Учебный год:** 2026/2027
- **Платформа:** Google Cloud

## Структура репозитория

```text
lab1/  lab1_report.md, images/
lab2/  lab2_report.md, images/
lab3/  lab3_report.md, images/
lab4/  lab4_report.md, diagrams/
```

Каждая работа лежит в своей папке `labN`: отчёт `labN_report.md` и скриншоты в `images/`.

## Лабораторные работы

| № | Тема | Статус | Отчёт |
|---|------|--------|-------|
| 1 | Обзор Google Cloud и исследование основных сервисов | Выполнена, отчёт готов | [lab1/lab1_report.md](lab1/lab1_report.md) |
| 2 | Исследование Cloud Run | Не выполнена | [lab2/lab2_report.md](lab2/lab2_report.md) |
| 3 | Исследование Cloud Storage | Не выполнена | [lab3/lab3_report.md](lab3/lab3_report.md) |
| 4 | Разработка инфраструктуры MVP AI-приложения | Не выполнена | [lab4/lab4_report.md](lab4/lab4_report.md) |

## Краткое содержание

**Лаба 1.** Создан service account и Spot-ВМ типа e2-micro, по SSH скопированы файлы из бакета, затем роль service account изменена со Storage Admin на Compute Viewer. Копирование при этом продолжало работать, потому что бакет публичный. Разницу ролей показала команда, требующая права на список бакетов. Все созданные ресурсы удалены.

**Лаба 2.** Развёртывание сервиса в Cloud Run, смена порта, распределение трафика между ревизиями.

**Лаба 3.** Создание бакета в Cloud Storage, организация объектов, публичный доступ.

**Лаба 4.** Проектирование инфраструктуры MVP AI-приложения по трём этапам и расчёт стоимости.

## Источники

- [Сайт курса и описания лабораторных](https://ex-itmo-ict-faculty.github.io/cloud-platforms-as-the-basis-of-technology-entrepreneurship/education/labs/)
- [Правила оформления отчётов](https://ex-itmo-ict-faculty.github.io/cloud-platforms-as-the-basis-of-technology-entrepreneurship/education/labs2023-2024/reportdesign/)
- [Документация Google Cloud](https://cloud.google.com/docs)
