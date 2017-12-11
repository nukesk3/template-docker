# template-docker

## 作成
```
$ docker-compose run --rm web rails new . --force --database=mysql --skip-bundle
$ docker-compose build
```

## db接続
config/database.yml
```
default: &default
  adapter: mysql2
  encoding: utf8
  pool: 5
  username: root
  password: <%= ENV['MYSQL_ROOT_PASSWORD'] %>
  host: db

development:
  <<: *default
  database: myapp_development

test:
  <<: *default
  database: myapp_test
```

## db生成
```
$ docker-compose up

$ docker-compose run --rm web rake db:create
```

## scaffold
```
$ docker-compose down
$ docker-compose run --rm web rails g scaffold item name:string amount:integer memo:text
$ docker-compose run --rm web rake db:migrate
$ docker-compose up -d

http://localhost:3000/items
```
