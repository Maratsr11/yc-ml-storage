# 05. Подключение DVC к Object Storage
## 1. Инициализация DVC

Если в проекте ещё нет DVC, выполните:
```Bash
dvc init
git add .dvc .gitignore
git commit -m "Initialize DVC"
```

## 2. Добавление remote
```Bash
dvc remote add -d yandex-s3 s3://<имя-бакета>/dvc-storage
dvc remote modify yandex-s3 endpointurl https://storage.yandexcloud.net
```

Замените <имя-бакета> на реальное имя вашего бакета.

## 3. Указание ключей доступа

Ключи лучше указывать локально, чтобы они не попали в git:
```Bash
dvc remote modify --local yandex-s3 access_key_id <KEY_ID>
dvc remote modify --local yandex-s3 secret_access_key <SECRET_KEY>
```

## 4. Проверка работы
```Bash
dvc push
dvc pull
dvc status -c
```

## Рекомендуемая структура в бакете

+ dvc-storage/ — кэш DVC

+ datasets/ — датасеты

+ models/ — модели

+ experiments/ — артефакты экспериментов

## Важные замечания

+ Флаг --local обязателен при указании ключей.

+ Не коммитьте файл .dvc/config.local в git.

+ Для разных окружений (dev/prod) можно создать несколько remote.
