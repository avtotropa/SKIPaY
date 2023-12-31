# <img src="img/SKIPaY.png" width="89"/> 
# SKIPaY

## "Платформа для публикации платного контента"


Реализована платформа для публикации записей пользователей. Публикация может быть бесплатной, доступна любому пользователю без регистрации и платной, доступна только авторизованным пользователям, который оплатили разовую подписку. Для реализации оплаты подписки используется эквайринг [Stripe](https://stripe.com/docs/api). Регистрация пользователя по номеру телефона.

***
### Прежде чем начать использовать проект нужно:
* Установить на ПК пакет docker
* Создать файл `.env` для переменного окружения.

### `.env`
    ALLOWED_HOSTS=*
    LANGUAGE_CODE=ru-ru
    TIME_ZONE=Europe/Moscow
    STRIPE_API_KEY=<STRIPE_API_KEY>
    POSTGRES_DB=skipay
    POSTGRES_USER=skipay
    POSTGRES_PASSWORD=skipay
    DATABASES_HOST=db

***
### Запуск Docker проекта
    git clone https://github.com/avtotropa/SKIPaY.git
    cd SKIPaY
    poetry install
    vi .env
    docker run -d --name redis -p 6379:6379 redis:7.0.5-alpine
    docker run -d --name db -e POSTGRES_USER=skipay -e POSTGRES_PASSWORD=skipay -e POSTGRES_DB=skipay -p 5432:5432 postgres
    python manage.py migrate
    python manage.py csu     
    python manage.py runserver <IP>:<PORT>
    celery -A config worker -l INFO
    celery -A config beat -l INFO --scheduler django_celery_beat.schedulers:DatabaseScheduler

***
#### P.S:
* будет добавлена учетная запись `+77777777777 12345` что бы войти в админку
* если команды будут выполняться с ошибкой прошу использовать повышение прав `sudo`
* весь проект выполняется в виртуальной среде `poetry shell`
