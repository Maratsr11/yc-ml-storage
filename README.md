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

* [Настройка DVC](docs/05-dvc-setup.md)


## Рекомендуемая структура в бакете

```text
your-bucket/
├── dvc-storage/       # кэш DVC
├── datasets/          # датасеты
├── models/            # модели
└── experiments/       # артефакты экспериментов
```

## Полезные ссылки

* [Документация Object Storage](https://yandex.cloud/docs/storage/)
* [S3 Connector в DataSphere](https://yandex.cloud/docs/datasphere/operations/data/s3-connectors)
* [DVC + S3-compatible storage](https://dvc.org/doc/user-guide/data-management/remote-storage/amazon-s3)
* [Калькулятор цен Yandex Cloud](https://yandex.cloud/prices)
