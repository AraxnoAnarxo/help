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

# forced push to git
git push -f --set-upstream origin master

# git if push requires pull...
 git pull --allow-unrelated-histories
 
# terminal bash - добавить bin
$ ln -s "/Applications/Sublime Text.app/Contents/SharedSupport/bin/subl" /usr/local/bin/sublime
открыть $ sublime workspace/site/index.html

# делаем откат изменений в репозитории для примера на два коммита назад
git reset --hard HEAD~2

# последние 10 комитов смотреть
git log --oneline -10

# heroku 
heroku apps:rename newname --app oldname

# POSTGRES

# пример подключения к Postgresql
psql -h localhost -U postgres -d postgres

# посмотеть, какие есть базы данных
\l;

# создать базу данных shop
create database shop;

# приконнектиться к базе данных shop
\c shop;

# посмотреть, что есть в базе данных
\d;

# создать таблицу customer с автоинкрементом id
create table customer(id serial promary key, name varchar(255), phone varchar(30), email varchar(20)));

# посмотреть таблицу customer
\d customer;

# содать таблицу product
create table product(id serial primary key, name varchar(255), description text, price integer);

# создать таблицу product_photo (связь с product)
create table product_photo(id serial primary key, url varchar(255), product_id integer references product(id));

# создать таблицу cart (ссылается на customer)
create table cart(customer_id integer references customer(id), id serial primary key);

# отношение многие ко многим (корзина(заказ) - товары в заказе)
create table cart_product(cart_id integer references cart(id), product_id integer references product(id));

# создать покупателя (customer)
insert into customer(name, phone, email) values ('Василий', '02', 'vas@mail.ru');
insert into customer(name, phone, email) values ('Петр', '03', 'petr@mail.ru');

# выбрать всех из таблицы customer
select * from customer;

# \x
Expanded display is on.
# \x
Expanded display is off.

# вставить продукты
insert into product (name, description, price) values ('iPhone','крутой телефон', 100000);
insert into product (name, description, price) values ('iWatch','крутые часы', 80000);

# вставить фото продуктов
insert into product_photo(url, product_id) values ('iphone_photo', 1);

# соединить две таблицы (конкретные поля) - url и название товара (с исп. алиасов)
select pp.*, p.name from product_photo pp left join product p on pp.product_id = p.id;

# удалить первичный ключ
alter table product_photo drop constraint product_photo_product_id_fkey;

# удалить строку в таблице
delete from product_photo where id = 2;

# обновить строку в таблице
update product_photo set url='iphone_image_2' where id=1;

# создать заказ
insert into cart(customer_id) values (1);

# создать сразу два товара в корзине
insert into cart_product (cart_id, product_id) values (1,1), (1,2);

# имена клиентов с общей суммой их заказов (name, общая сумма заказов)
# 1 - все покупатели и их заказы со стоимостью продуктов
select c.name, cart.id as cart_id, cp.product_id, p.price from customer c left join cart on cart.customer_id = c.id left join cart_product cp on cp.cart_id = cart.id left join product p on p.id=cp.product_id;
# 2 - просуммировать price по всем покупателям, вывести суммарный price каждого покупателя (group by name, sum(price))
select c.name, sum(p.price) from customer c left join cart on cart.customer_id = c.id left join cart_product cp on cp.cart_id = cart.id left join product p on p.id=cp.product_id group by c.name;
# 3 - заменить null на другое значение с пом. coalesce
select c.name, coalesce(sum(p.price),0) as order_sum from customer c left join cart on cart.customer_id = c.id left join cart_product cp on cp.cart_id = cart.id left join product p on p.id=cp.product_id group by c.name;
# 4 - отсортировать по сумме;
select c.name, coalesce(sum(p.price),0) as order_sum from customer c left join cart on cart.customer_id = c.id left join cart_product cp on cp.cart_id = cart.id left join product p on p.id=cp.product_id group by c.name order by order_sum desc;
# 5 - выбрать только тех клиентов, которые что-то купили (having фильтрует группы)
select c.name, coalesce(sum(p.price),0) as order_sum from customer c left join cart on cart.customer_id = c.id left join cart_product cp on cp.cart_id = cart.id left join product p on p.id=cp.product_id group by c.name having sum(p.price)> 0;

# limit, order by (если проблемы с кодировкой - использовать using ~<~)
select * from customer order by name using ~<~;
