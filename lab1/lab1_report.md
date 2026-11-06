University: [ITMO University](https://itmo.ru/ru/)
Faculty: [FICT](https://fict.itmo.ru)
Course: [Cloud platforms as the basis of technology entrepreneurship](https://github.com/itmo-ict-faculty/cloud-platforms-as-the-basis-of-technology-entrepreneurship)
Year: 2026/2027
Group: U4225
Author: Kaasamani Roni Bahaaevich
Lab: Lab1
Date of create: 03.11.2026
Date of finished: 06.11.2026

# Лабораторная работа №1. Обзор Google Cloud и исследование основных сервисов

## Цель работы

Познакомиться с основными возможностями и преимуществами облачной платформы Google Cloud.

## Ход работы

Все действия выполнялись 03.11.2026 в консоли Google Cloud, проект `cloud-platforms-as-the-basis`.

### 1. Доступ и service account

Доступ к проекту получен через Google-форму курса. В IAM & Admin → Service Accounts создан service account `rkaasamani-sa-lab1` (первая буква имени + фамилия + `-sa-lab1`). В IAM ему назначена роль **Storage Admin**.

![Service account в списке](images/01-service-account.jpg)

![Роль Storage Admin](images/02-sa-role-storage-admin.jpg)

### 2. Виртуальная машина

Создана ВМ `rkaasamani-vm-lab1` в Compute Engine: серия E2, тип **e2-micro**, модель выделения **Spot**, регион us-central1. Для ВМ указан service account `rkaasamani-sa-lab1` и доступ «Allow full access to all Cloud APIs», чтобы права определялись только ролью в IAM, а не ограничениями scopes.

![Параметры ВМ: e2-micro, Spot](images/03-vm-config-spot-e2micro.jpg)

![Service account и scopes](images/04-vm-service-account.jpg)

![ВМ в статусе Running](images/05-vm-running.jpg)

### 3. Копирование файлов из бакета `lab1-bucket-itmo`

Подключение выполнено через SSH-in-browser. Команды:

```bash
gcloud storage ls gs://lab1-bucket-itmo
mkdir -p ~/lab1_files
gcloud storage cp gs://lab1-bucket-itmo/pic1.jpg gs://lab1-bucket-itmo/pic2.jpg gs://lab1-bucket-itmo/pic3.jpeg ~/lab1_files/
ls -lah ~/lab1_files
```

В бакете три файла: `pic1.jpg`, `pic2.jpg`, `pic3.jpeg`. Все они скопированы на ВМ (общий размер около 1,5 МиБ).

![Содержимое бакета](images/06-bucket-listing.jpg)

![Копирование и ls -lah](images/07-cp-and-ls.jpg)

### 4. Смена роли на Compute Viewer

В IAM у `rkaasamani-sa-lab1` роль Storage Admin заменена на **Compute Viewer**. Консоль сообщила «Policy updated. It may take a few minutes for these changes to become active».

![Выбор роли Compute Viewer](images/08-role-change-compute-viewer.jpg)

![Роль изменена](images/09-role-compute-viewer-saved.jpg)

Через ~1,5 минуты и затем ещё раз через ~5 минут копирование было повторено в новые каталоги (`~/lab1_files_2`, `~/lab1_files_3`). **Копирование снова прошло успешно**, ошибки 403 не было.

![Повторное копирование, попытка 1](images/10-cp-after-role-change-1.jpg)

![Повторное копирование, попытка 2 (через ~5 минут)](images/12-cp-after-role-change-2.jpg)

#### Проверка причины

1. Команда `gcloud auth list` показывает, что на ВМ активна учётная запись `rkaasamani-sa-lab1`. Чтение IAM-политики бакета этой учётной записи уже запрещено (`storage.buckets.getIamPolicy` denied), то есть новая роль действует.

   ![Активная учётная запись и отказ в getIamPolicy](images/11-auth-list-iam-denied.jpg)

2. Анонимный запрос без авторизации `curl -sI https://storage.googleapis.com/lab1-bucket-itmo/pic1.jpg` возвращает `HTTP/2 200`. Значит, **объекты бакета доступны публично**, и для их чтения роль service account не нужна. Поэтому смена Storage Admin → Compute Viewer не повлияла на копирование.

   ![Анонимный доступ: HTTP 200](images/13-anonymous-http-200.jpg)

#### Сравнение ролей по операции, зависящей от роли

Чтобы показать реальную разницу между ролями, использована операция, требующая права `storage.buckets.list`:

```bash
gcloud storage buckets list --project=cloud-platforms-as-the-basis --format="value(name)"
```

- Под ролью **Compute Viewer**: `HTTPError 403 ... does not have storage.buckets.list access`.

  ![Compute Viewer: 403](images/14-buckets-list-denied.jpg)

- Затем роль временно возвращена на **Storage Admin** (для сравнения), после ~1,5 минут та же команда выполнена успешно и вернула имя бакета `lab1-bucket-itmo`.

  ![Роль Storage Admin возвращена](images/15-role-storage-admin-restored.jpg)

  ![Storage Admin: команда выполняется](images/16-buckets-list-ok.jpg)

Порядок проверок: сначала зафиксирован отказ под Compute Viewer, затем роль возвращена на Storage Admin и получен успех.

### 5. Удаление ресурсов

Удалены ВМ `rkaasamani-vm-lab1` (вместе с загрузочным диском) и service account `rkaasamani-sa-lab1`. Служебные ресурсы других участников не затрагивались.

![Список ВМ пуст](images/17-cleanup-vm-deleted.jpg)

![Service account удалён](images/18-cleanup-sa-deleted.png)

## Выводы

- **Service account** — это идентификатор приложения или ВМ, а не человека. ВМ получает доступ к облачным API под его ролями, поэтому ключи в виде файлов не нужны.
- **Роль определяет, что разрешено.** Storage Admin разрешает, в частности, перечислять бакеты и читать IAM-политику бакета. Compute Viewer даёт только просмотр ресурсов Compute Engine, а к Cloud Storage доступа не даёт. Это видно по ошибке 403 на `buckets list`.
- **Принцип наименьших привилегий:** сервисному аккаунту выдают только те права, которые нужны задаче.
- **Права на объект не всегда задаются ролью аккаунта.** Бакет `lab1-bucket-itmo` публичен, поэтому его файлы читаются даже без прав, и копирование не зависело от роли. Эффект смены роли надо проверять на операции, которая действительно требует этой роли.
- **Изменения IAM применяются не мгновенно:** консоль предупреждает, что нужно подождать несколько минут.
- **Spot-ВМ** дешевле обычной, но может быть остановлена платформой, поэтому подходит для некритичных задач. Все созданные ресурсы удалены, чтобы не было лишних расходов.
