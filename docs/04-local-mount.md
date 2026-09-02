04. Локальное монтирование бакета
Есть несколько способов смонтировать бакет Object Storage как обычную папку на компьютере.
Вариант 1: s3fs (самый простой)
Установка
Ubuntu / Debian:
Bashsudo apt update
sudo apt install s3fs
macOS:
Bashbrew install s3fs
Настройка ключей
Bashecho "KEY_ID:SECRET_KEY" > ~/.passwd-s3fs
chmod 600 ~/.passwd-s3fs
Монтирование
Bashmkdir -p ~/mnt/ml-artifacts

s3fs <имя-бакета> ~/mnt/ml-artifacts \
  -o passwd_file=$HOME/.passwd-s3fs \
  -o url=https://storage.yandexcloud.net \
  -o use_path_request_style \
  -o allow_other
Размонтирование
Bashfusermount -u ~/mnt/ml-artifacts
Вариант 2: rclone (кроссплатформенный)
Настройка
Bashrclone config
При настройке укажите:

Тип хранилища: s3
Provider: Other
Endpoint: https://storage.yandexcloud.net
Access Key ID и Secret Access Key — от вашего сервисного аккаунта

Монтирование
Bashrclone mount yc:<имя-бакета> ~/mnt/ml-artifacts --vfs-cache-mode full
Вариант 3: GeeseFS (рекомендуется Yandex)
GeeseFS обычно работает быстрее и стабильнее, чем s3fs.
Скачать можно здесь:

https://github.com/yandex-cloud/geesefs
После скачивания бинарника пример команды монтирования:
Bash./geesefs \
  --endpoint https://storage.yandexcloud.net \
  <имя-бакета> \
  ~/mnt/ml-artifacts
