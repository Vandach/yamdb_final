![This is an image](https://github.com/Vandach/yamdb_final/actions/workflows/yamdb_workflow.yml/badge.svg)

### Проект api_yamdb:

Проект api_yamdb позволяет собирать отзывы на Книги, Фильмы и Музыка. Пользователи зарегистрированные на проекте, могут сами делать отзывы, оставлять комментарии и ставить оценки.

При внесении изменений в проект он автоматически проходит тесты. Если ошибок нет, происходит запись или обновление образа на Docker Hub. Затем обнавлёная версия отправляется и запускается на сервере. По итогу еси всё прошло хорошо, Вы получите уведомление в Telegram.

### Как запустить проект:

Сделайте Fork проекта в свой репозитарий.

Откройте командную строку.

Клонируйте репозиторий:

```
git clone git@github.com:{ваш Ник на github}/yamdb_final.git
```

На github добавьте в Settings Secrets значения: 

SECRET_KEY= {секретный ключ Django}  
USER= {имя для подключения к серверу}  
HOST= {IP сервера}  
PASSPHRASE= {пароль при подключении к серверу (если есть)}  
SSH_KEY= {SSH ключ для подключения к серверу}  
TELEGRAM_TO= {id телеграма куда будет приходить результат проверки на github}  
TELEGRAM_TOKEN= {токен Вашего бота телеграм, который будет отвечать за отправку результатов проверки}  
DOCKER_USERNAME= {Ваш Ник на Docker Hub}  
DOCKER_PASSWORD= {Ваш пароль на Docker Hub}  
DB_ENGINE= {django.db.backends.postgresql}  
DB_NAME= {postgres}  
DB_USER= {postgres}  
DB_PASSWORD= {postgres}  
DB_HOST= {db}  
DB_PORT= {5432}  

Установите на своём сервере Docker и Docker-Compose.

Выполните Push проекта на GitHub.

Подключитесь к серверу и проверьте работу контейнеров:

```
sudo docker ps -a
```

Выполните команды:

```
sudo docker exec {имя контейнера web} python manage.py makemigrations
sudo docker exec {имя контейнера web} python manage.py migrate
sudo docker exec {имя контейнера web} python manage.py collectstatic --no-input
```

Там же в терминале создайте Суперюзера:

```
sudo docker exec -it {имя контейнера web} python manage.py createsuperuser
```

Войти в проект можно перейдя на страницу http://{IP сервера}/admin/


### Примеры запросов:

Вывод произведений:
```
http://{IP сервера}/api/v1/titles/
```

Вывод отзывов:
```
http://{IP сервера}/api/v1/titles/{title_id}/reviews/
```

Вывод комментариев:
```
http://{IP сервера}/api/v1/titles/{title_id}/reviews/{review_id}/
```

Вывод пользователей:
```
http://{IP сервера}/api/v1/users/
```

С документацией к проекту можно ознакомиться на странице http://{IP сервера}/redoc/


### Автор:

Студент Яндекс Практикум 

Кирилл Аль-Шаер
