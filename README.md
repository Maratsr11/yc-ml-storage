<div align="center">

# Yandex Cloud ML Storage

**Практическое руководство по организации хранилища артефактов, моделей и датасетов**  
для ML-команд с использованием **Yandex Object Storage**, **DataSphere** и **DVC**

[![Yandex Cloud](https://img.shields.io/badge/Yandex%20Cloud-Object%20Storage-red?style=flat-square)](https://yandex.cloud)
[![DataSphere](https://img.shields.io/badge/DataSphere-S3%20Connector-blue?style=flat-square)](https://yandex.cloud/services/datasphere)
[![DVC](https://img.shields.io/badge/DVC-Compatible-purple?style=flat-square)](https://dvc.org)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg?style=flat-square)](LICENSE)

</div>

---

## Что внутри?

Полная инструкция по созданию надёжного хранилища для ML-команды:

* Создание **Object Storage** (S3)
* Настройка сервисного аккаунта и статических ключей
* Подключение бакета к проекту **DataSphere** через S3 Connector
* Локальное монтирование (s3fs / GeeseFS / rclone)
* Интеграция с **DVC**
* Рекомендации по структуре хранения

## Быстрый старт

### 1. Создайте бакет и сервисный аккаунт

* [Создание бакета](docs/01-create-bucket.md)
* [Сервисный аккаунт и ключи](docs/02-service-account.md)

### 2. Подключите бакет к DataSphere

* [S3 Connector](docs/03-datasphere-connector.md)

### 3. Настройте локальный доступ (по желанию)

* [Локальное монтирование](docs/04-local-mount.md)

### 4. Подключите DVC

```bash
dvc remote add -d yandex-s3 s3://<имя-бакета>/dvc-storage
dvc remote modify yandex-s3 endpointurl https://storage.yandexcloud.net

# Ключи храните локально
dvc remote modify --local yandex-s3 access_key_id <KEY_ID>
dvc remote modify --local yandex-s3 secret_access_key <SECRET_KEY>
