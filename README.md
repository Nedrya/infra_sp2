### О проекте:

Данный проект является классическим примером отзовика с API и контейнерезацией Docker.
В качестве фреймворка использовался Django 2.2.16.
В качестве контейнера Docker Desktop 4.12.0 
Дополнительно использовались следующие пакеты: Django-filter 22.1, Django REST framework 3.12.4, Simple JWT 4.7.2, Gunicorn 20.0.4.


### Как запустить проект:

Клонировать репозиторий и перейти в него в командной строке:

```
git clone https://github.com/Nedrya/infra_sp2
```

```
Скачиваем https://www.docker.com/ и устанавливаем Docker.
```

Создайте файл переменного окружения:

```
cd infra_sp2\infra
```

```
touch .env
```

Настройте переменных окружения:

```
DB_ENGINE = <Ваше_значение>
DB_NAME = <Ваше_значение>
POSTGRES_USER = <Ваше_значение>
POSTGRES_PASSWORD = <Ваше_значение>
DB_HOST = <Ваше_значение>
DB_PORT = <Ваше_значение>
SECRET_KEY = <Ваше_значение>
```

Разворачиваем проект запущенный через Gunicorn с базой данных Postgres:

```
docker-compose up
```

Выполняем миграции:

```
docker-compose exec web python manage.py migrate
```

Создаем суперпользователя:

```
wimpty docker-compose exec web python manage.py createsuperuser
```

Собираем статические файлы:

```
docker-compose exec web python manage.py collectstatic --no-input 
```


### Информация:

Регистрация:
Регистрация происходит путем отправки POST запроса с указание пользовательского имени и адреса электронной почты.

Пример запроса регистрации нового пользрвателя:
```
POST http://127.0.0.1:8000/api/v1/auth/signup/
Content-Type: application/json

{
    "username": "1112",
    "email": "1112@qwe.ru"
}
```

Пример ответа:
```
{
  "email": "1112@qwe.ru",
  "username": "1112"
}
```

После успешной регистрации на почту придет секретный код, который позволит подтвердить почту и получить токен аутентификации.
Пример секретного кода: MSBrKI8ZkD


Подтверждение адреса электронной почты и получение токена аутентификации:

Пример запроса:
```
POST http://127.0.0.1:8000/api/v1/auth/signup/
Content-Type: application/json

{
    "username": "1112",
    "confirmation_code": "MSBrKI8ZkD"
}
```

Пример ответа:
```
{
  "token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ0b2tlbl90eXBlIjoiYWNjZXNzIiwiZXhwIjoxNjU3NjEyMzg1LCJqdGkiOiJiNjI4N2Y3Y2JhMGQ0ZThjOGM3NGM2MTcwMDI4NjdkMCIsInVzZXJfaWQiOjEsInVzZXJuYW1lIjoiMTExMiIsImNvbmZpcm1hdGlvbl9jb2RlIjoiTVNCcktJOFprRCJ9.5wo80prs8WWwIZrsESG-fL9xl0jfNSYVq5mdFdpIVxs"
}
```

Подробнее с примерами запросов можно ознакомиться по ссылке http://127.0.0.1:8000/redoc/ .

Авторы проекта: Недря Сергей




