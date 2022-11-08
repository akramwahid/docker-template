#A Docker Setup with Containers for PHP, NGINX, MYSQL, ARTISAN, COMPOSER, NPM REDIS

#Usage

clone it using `git clone .....`

---
#1 __Spin up docker container__

make sure you have Docker System (Docker desktop for mac/windows) installed on your system.

in your terminal navigate to the directory where you cloned the project, and spin up the containers for nginx, php, mysql 
by running 

`docker-compose up -d --build app`. 

By default the mysql will run in port 3306, if you need to adjust the port or container names incase of conflicts, 
you can do it in `docker-compose.yml` file.

---


# __Install the Laravel Project__

 proceed and type the following commands in your terminal to install the project.

`docker-compose run --rm composer create-project laravel/laravel=8 /src`

---
  
# __Adjust Database Configuration__

default db user is `testuser` and password is `123456`, you can modify this in `docker-compose.yml`


make a copy of `.env.example` placed in the source code root `/src` and name it as `.env`.


in `.env` set db configurations, and make sure DB_HOST is set as mysql since our mysql container service is named as mysql

---

# __Running Database migration and seeding test data__

next run the following artisan command in terminal to setup the database tables

`docker-compose run --rm artisan migrate`

next run the following command to seed some test data in to the database (authors, posts, comments)

`docker-compose run --rm artisan db:seed`


*** if you want to rebuild database tables and seed fresh data, you can do it with 

`docker-compose run --rm artisan migrate:fresh --seed` ***



---

# __Create a symbolic link__

run the following command To make the uploaded files accessible from the web,
Following command will create a symbolic link from `public/storage` to `storage/app/public`
 
 `docker-compose run --rm artisan storage:link`
 

---

# __View the project in browser__

you can access the project in the url of `http://localhost:8087`

you can access the phpmyadmin database client in `http://localhost:8088`


# __Compiling frontend assets (Optional)__

This step is only required if you do any changes to the frontend code files

if you want rebuild frontend assets, you may run the following command to install npm modules

`docker-compose run --rm npm install`

and the run the following command to build the frontend in development environment 

`docker-compose run --rm npm run dev`


---

# __Testing with PHPUnit (Optional)__

I have added some test cases in the `/src/tests` directory 
To run the tests cases, execute following command

`docker-compose run --rm artisan test`

---

# __Useful commands __
`docker-compose run --rm artisan make:migration create_posts_table --create=posts`

`docker-compose run --rm artisan migrate`

`docker-compose run --rm artisan make:model Post`

`docker-compose run --rm artisan make:factory PostFactory`

`docker-compose run --rm artisan make:seeder TestDataSeeder`

`docker-compose run --rm artisan db:seed / ... db:seed --class=TestDataSeeder`

`docker-compose run --rm artisan make:test PostTest`

`docker-compose run --rm artisan make:resource PostResource`

`docker-compose run --rm artisan make:resource PostCollection`

`docker-compose run --rm artisan make:controller --model=Post --api --resource --request`

`docker-compose run --rm npm install vuex@3`