# API_YAMDB
REST API проект для сервиса YaMDb — сбор отзывов о фильмах, книгах или музыке.

## Описание

Проект YaMDb собирает отзывы пользователей на произведения.
Произведения делятся на категории: «Книги», «Фильмы», «Музыка».
Список категорий  может быть расширен (например, можно добавить категорию «Изобразительное искусство» или «Ювелирка»).
### Как запустить проект:

Все описанное ниже относится к ОС Linux.
Клонируем репозиторий и переходим в него:
```bash
git clone https://github.com/Abramow79/infra_sp2
cd infra_sp2
cd api_yamdb
```

Создаем и активируем виртуальное окружение:
```bash
python3 -m venv venv
source /venv/bin/activate (source /venv/Scripts/activate - для Windows)
python -m pip install --upgrade pip
```

Ставим зависимости из requirements.txt:
```bash
pip install -r requirements.txt
```

Переходим в папку с файлом docker-compose.yaml:
```bash
cd infra
```

Поднимаем контейнеры (infra_db_1, infra_web_1, infra_nginx_1):
```bash
docker-compose up -d --build
```

Выполняем миграции:
```bash
docker-compose exec web python manage.py makemigrations reviews
```
```bash
docker-compose exec web python manage.py migrate
```

Создаем суперпользователя:
```bash
docker-compose exec web python manage.py createsuperuser
```

Србираем статику:
```bash
docker-compose exec web python manage.py collectstatic --no-input
```

Создаем дамп базы данных (нет в текущем репозитории):
```bash
docker-compose exec web python manage.py dumpdata > dumpPostrgeSQL.json
```

Останавливаем контейнеры:
```bash
docker-compose down -v
```

### Шаблон наполнения .env (не включен в текущий репозиторий) расположенный по пути infra/.env
```
DB_ENGINE=django.db.backends.postgresql
DB_NAME=postgres
POSTGRES_USER=postgres
POSTGRES_PASSWORD=postgres
DB_HOST=db
DB_PORT=5432
```

### Документация API YaMDb
Документация доступна по эндпойнту: http://localhost/redoc/

#### Autor
Andrey Abramov 

## Used technologies
* [Python](https://www.python.org/)
* [Django](https://www.djangoproject.com/)
* [Django REST framework](https://www.django-rest-framework.org/)
* [DRF Simple JWT](https://django-rest-framework-simplejwt.readthedocs.io/en/latest/)

## Useful links

- [DRF Routing](https://www.django-rest-framework.org/api-guide/routers/)
- [DRF Permissions](https://www.django-rest-framework.org/api-guide/permissions/)
- [DRF Filtering and Search](https://www.django-rest-framework.org/api-guide/filtering/)
- [DRF Testing](https://www.django-rest-framework.org/api-guide/testing/)
- [Factory_boy & Django ORM](https://factoryboy.readthedocs.io/en/latest/orms.html#django)
- [Faker: test data generation](https://faker.readthedocs.io/en/master/providers.html)
- [Data migrations](https://docs.djangoproject.com/en/4.1/topics/migrations/)
- [Custom management program](https://docs.djangoproject.com/en/4.1/howto/custom-management-commands/)
- [drf-yasg: OpenAPI Specification generator](https://drf-yasg.readthedocs.io/en/stable/)
- [Django-filters](https://django-filter.readthedocs.io/en/stable/guide/usage.html#declaring-filters)
