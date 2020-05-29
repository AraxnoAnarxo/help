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

# установить psycopg2
python -m pip install psycopg2-binary

# MySql подключение к базе через доп. модуль
pip install pymysql
SQLALCHEMY_DATABASE_URI = 'mysql+pymysql://.....'

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

