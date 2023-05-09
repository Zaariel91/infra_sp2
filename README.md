## Описание

Проект предназначен для оценки книг, музыки и фильмов различных жанров. 
Данный проект позволяет написать рецензию на произведение, а также оставить отзыв с присвоением оценки. 

## Установка

1. Проверьте наличие Docker

   Убедитесь, что docker установлен на вашем устройстве выполнив команду:

   ```bash
   docker -v
   ```

   В случае отсутствия, скачать [Docker Desktop](https://www.docker.com/products/docker-desktop) для Mac или Windows. [Docker Compose](https://docs.docker.com/compose) будет установлен автоматически.

   Для Linux выполните следующие команды:
   
   ```bash
   sudo apt install curl
   curl -fsSL https://get.docker.com -o get-docker.sh
   sh get-docker.sh  
   ```
   При необходимости воспользуйтесь официальной [инструкцией](https://docs.docker.com/engine/install/).

2. Клонируйте репозиторий на локальный компьютер

   ```bash
   git clone git@github.com:Zaariel91/infra_sp2.git
   ```

3. В корневой директории создайте файл `.env`, согласно шаблону:

   ```bash
   DB_ENGINE=django.db.backends.postgresql
   DB_NAME=postgres
   POSTGRES_USER=postgres
   POSTGRES_PASSWORD=postgres
   DB_HOST=db
   DB_PORT=5432
   ```
   Также в файле укажите переменную `SECRET_KEY` со своим ключом. 
   При необходимости сгенерируйте новый ключ (https://djecrety.ir/)

4. Запустите `docker-compose`

   Выполните из корневой директории команду:

   ```bash
   docker-compose up -d
   ```

5.  Выполните миграции

   ```bash
   docker-compose exec web python manage.py makemigrations
   docker-compose exec web python manage.py migrate
   ```

6. Подгрузите статику для отображения стилей и картинок

   ```bash
   docker-compose exec web python manage.py collectstatic --no-input
   ```

7. Заполните БД тестовыми данными из файла `fixtures.json`.

   В директории `infra_sp2`. Выполните команду:

   ```bash
   docker-compose exec web python manage.py loaddata fixtures.json
   ```

8. Создайте суперпользователя

   ```bash
   docker-compose exec web python manage.py createsuperuser
   ```

9. Зайдите на (http://localhost/admin/) и убедитесь, что страница отображается полностью: статика подгрузилась;
   Авторизуйтесь под аккаунтом суперпользователя и убедитесь, что миграции прошли успешно.
   
Проект запущен. Удачной работы.
