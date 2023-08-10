## Задание 27.1 Основы Docker
### Задание 1
    Установите Docker.

### Задание 2
    Создайте контейнер с подходящей версией Python и убедитесь, что проект запускается и корректно работает.

    Условия проверки работы:

    контейнер для Django-проекта запускается,
    на хостовой машине открывается стартовая страница проекта.
-   создаем новый образ с python и bash

docker run --network host -it python bash

создался контйнер с id a8cd530ffc81

-   устанавливаем django

pip install django
-   создаем новый проект project

mkdir project

cd project

django-admin startproject config .

python manage.py startapp app

- запускаем проект

python manage.py makemigrations

python manage.py migrate

python manage.py runserver


### Задание 3
    Создайте контейнер, в котором будет развернута БД PostgreSQL. Создайте локально папку, в которую будут размещаться данные базы.

    * Дополнительное задание
    Разверните в Docker Redis для работы с очередями и подключите его к текущему проекту.

-   Создаем контейнер с именем domz_27_1 с базой postgres с названием test, логин postgres, пароль postgres, директория для обмена с БД c:/users/fastpost/docker_test/

docker run --name domz_27_1 -p 5432:5432 -e POSTGRES_USER=postgres -e POSTGRES_PASSWORD=postgres -e POSTGRES_DB=test  -e POSTGRES_HOST_AUTH_METHOD=md5 -v c:/users/fastp/docker_test/pgdata:/var/lib/postgresql/data/ postgres


__в другом терминале:__

-   смотрим, какие контейнеры запущены

    docker ps -a

-   подключаемся к базе данных postgres в контейнере  domz_27_1

    docker exec -it domz_27_1 psql -U postgres

-   база test создана
-   подключаем локальную сеть к контейнеру, устанавливаем python и подключаемся через bash

    docker run --network host -it python bash

-   устанавливаем django, psycopg2

    pip install django

    pip install psycopg2

-   создаем новый проект project

mkdir project

cd project

django-admin startproject config .

python manage.py startapp app

-   устанавливаем редактор nano

apt-get update

apt-get install nano

-   редактируем файл settings.py

nano config/settings.py

-   вносим настройки БД

DATABASES = {

    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': 'test',
        'USER': 'postgres',
        'PASSWORD': 'postgres',
        'HOST': '127.0.0.1',
        'PORT': '5432',
    }
}

- запускаем проект

python manage.py makemigrations

python manage.py migrate

python manage.py runserver

-   устанавливаем redis

apt install redis-server -y

service redis-server start
-   проверяем

redis-cli ping

Ответ:
PONG
