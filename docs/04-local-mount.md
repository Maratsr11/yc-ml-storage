# 04. Локальное монтирование бакета

Есть несколько способов смонтировать бакет Object Storage как обычную папку на компьютере. Ниже приведены три основных варианта.

## Вариант 1: s3fs
Самый простой способ для Linux и macOS.
Установка
**Ubuntu / Debian:**
```Bash
sudo apt update
sudo apt install s3fs
```
**macOS:**
```Bash
brew install s3fs
```
**Настройка ключей**

Создайте файл с ключами доступа:
```Bash
echo "KEY_ID:SECRET_KEY" > ~/.passwd-s3fs
chmod 600 ~/.passwd-s3fs
```
Замените KEY_ID и SECRET_KEY на реальные значения статического ключа сервисного аккаунта.


**Монтирование**
```Bash
mkdir -p ~/mnt/ml-artifacts

s3fs <имя-бакета> ~/mnt/ml-artifacts \
  -o passwd_file=$HOME/.passwd-s3fs \
  -o url=https://storage.yandexcloud.net \
  -o use_path_request_style \
  -o allow_other
```
После выполнения команды бакет будет доступен в папке ~/mnt/ml-artifacts.


**Размонтирование**
```Bash
fusermount -u ~/mnt/ml-artifacts
```

## Вариант 2: rclone
Удобный кроссплатформенный инструмент (Linux, macOS, Windows).

**Настройка**

Запустите конфигурацию:
```Bash
rclone config
```

При настройке укажите следующие параметры:

Тип хранилища: s3

Provider: Other

Endpoint: https://storage.yandexcloud.net

Access Key ID — идентификатор статического ключа

Secret Access Key — секретный ключ

**Монтирование**
```Bash
rclone mount yc:<имя-бакета> ~/mnt/ml-artifacts --vfs-cache-mode full
```
Где yc — имя remote, которое вы задали при настройке.


## Вариант 3: GeeseFS
Рекомендуемый способ от Yandex. Обычно работает быстрее и стабильнее, чем s3fs.

Скачать бинарник можно здесь: https://github.com/yandex-cloud/geesefs

**Пример монтирования**
```Bash
./geesefs \
  --endpoint https://storage.yandexcloud.net \
  <имя-бакета> \
  ~/mnt/ml-artifacts
```

## Рекомендации

+ Для повседневной работы чаще всего достаточно s3fs или rclone.

+ Если важна производительность при большом количестве мелких файлов — используйте GeeseFS.

+ Не храните файл ~/.passwd-s3fs в открытом доступе и не добавляйте его в git.
