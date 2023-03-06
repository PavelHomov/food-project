![workflow](https://github.com/PavelHomov/foodgram-project-react/actions/workflows/main.yml/badge.svg)
# Проект Foodgram - «Продуктовый помощник» 158.160.15.196
# доступ к админке login: hi password: hi
Онлайн-сервис и API для него. 
На этом сервисе пользователи смогут публиковать 
рецепты, подписываться на публикации других 
пользователей, добавлять понравившиеся рецепты в 
список «Избранное», а перед походом в магазин 
скачивать сводный список продуктов, необходимых 
для приготовления одного или нескольких выбранных блюд.

В проекте использована база PostgreSQL. Проект запускается
в четырех контейнерах на сервере.
Образ с проектом загружается на Docker Hub. Реализован 
CI/CD.

## Технологии

Python, Django, DRF, Docker, Docker-compose, PostgreSQL, nginx, Linux.

## Запуск проекта с помощью Docker

1. Склонируйте репозиторий.

    ```
    git clone git@github.com:PavelHomov/foodgram-project-react.git
    ```

2. Создайте .env файл 

    ```
    SECRET_KEY=Optional
    DB_ENGINE=django.db.backends.postgresql
    DB_NAME=postgres
    POSTGRES_USER=postgres
    POSTGRES_PASSWORD=postgres
    DB_HOST=db
    DB_PORT=5432
    HOST=<server_name>
    PORT=<port>
    UPSTREAM=<proxy_pass>
    ```

3. Перейдите в директорию infra/ и выполните команду для создания и запуска контейнеров.
    ```
    sudo docker compose up -d --build
    ```

    > В Windows команда выполняется без **sudo**

4. В контейнере app выполните миграции, создайте суперпользователя и соберите статику.

    ```
    sudo docker-compose exec backend python manage.py migrate
    sudo docker-compose exec backend python manage.py createsuperuser
    sudo docker-compose exec backend python manage.py collectstatic --no-input 
    ```

5. Загрузите в бд ингредиенты командой ниже.

    ```
    sudo docker-compose exec backend python manage.py load_ingredients
    ```

6. Готово:
    -  http://localhost/ - главная страница сайта;
    -  http://localhost/admin/ - админ панель;
    -  http://localhost/api/ - API проекта
    -  http://localhost/api/docs/redoc.html - документация к API

---
## Автор
**[Павел Хомов](https://github.com/PavelHomov)** 
