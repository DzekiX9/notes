## Ubuntu
### Установка venv (Virtual Environment)

``` bash
sudo apt install -y python3-venv
```
### Создание виртуальной среды для приложения

``` bash
mkdir myapp && cd myapp
python3 -m venv env
```
### Активация окружения виртуальной среды

``` bash
source env/bin/activate
```

### Деактивация виртуальной среды

``` bash
deactivate
```

### Автоматическая активация виртуальной среды при запуске приложения

Файл *myapp/run.sh* :
``` bash
#!/usr/bin/env bash

BASEDIR=$(dirname "$0")

echo "Executing App in '$BASEDIR'"

PORT=$1

source $BASEDIR/env/bin/activate

python $BASEDIR/service.py $PORT
```

Установим права на исполнение и протестируем его запуск:

``` bash
chmod +x myapp/run.sh

./myapp/run.sh 8888
```
