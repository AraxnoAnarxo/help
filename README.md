# help
commands etc

# создать виртуальную среду в проекте
python3 -m venv <...>

# зайти в виртуальную среду
source <...>/bin/activate 

# создать файл с требованиями к виртуальной среде
pip freeze > requirements.txt

# установить модули из requirements.txt на сервере
pip install -r requirements.txt

# список всех вирт. сред (Lnux)
lsvirtualenv

# список всех модулей, установленных в вирт. среде (Linux)
lssitepackages

# установить psycopg2
python -m pip install psycopg2-binary

# MySql подключение к базе через доп. модуль
pip install pymysql
SQLALCHEMY_DATABASE_URI = 'mysql+pymysql://.....'

# коннектор MySQL
mysql-connector-python

# Создать проект в Django
django-admin startproject ///

# Создать приложение в Django
django-admin startapp ///

# Создать образ в Docker
docker build -t <name:tag> .

# Поднять контейнер в Docker
docker run -d -p 5000:5000 <name:tag>

# залогиниться в Docker
docker login

# Переименовать образ в Docker
docker tag <oldname> <newname>
  
# Сделать push в Docker
docker push <name>
  
# мирграции Django docker-compose
docker-compose run web python /code/manage.py makemigrations --noinput

# запуск контейнера Docker docker-compose
docker-compose up -d --build

# запуск Docker Postgresql
docker run --rm   --name pg-docker -e POSTGRES_PASSWORD=docker -d -p 5432:5432 -v $HOME/docker/volumes/postgres:/var/lib/postgresql/data  postgres

docker run --name test_postgres -e POSTGRES_PASSWORD=password1 -d postgres

# пример подключения к Postgresql Docker
docker exec -it test_postgres psql -U postgres

# пример подключения к Postgresql
psql -h localhost -U postgres -d postgres

# forced push to git
git push -f --set-upstream origin master

# git if push requires pull...
 git pull --allow-unrelated-histories
 
# terminal bash - добавить bin
$ ln -s "/Applications/Sublime Text.app/Contents/SharedSupport/bin/subl" /usr/local/bin/sublime
открыть $ sublime workspace/site/index.html



