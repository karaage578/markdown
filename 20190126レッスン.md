sudo apt remove postgresql-*



ii  postgresql-client                          10+190                                       all          front-end programs for PostgreSQL (supported version)
ii  postgresql-client-10                       10.6-0ubuntu0.18.04.1                        amd64        front-end programs for PostgreSQL 10
ii  postgresql-client-common                   190                                          all          manager for multiple PostgreSQL client versions
ii  postgresql-common                          190                                          all          PostgreSQL database-cluster manager
ii  postgresql-server-dev-all                  190                                          all          extension build tool for multiple PostgreSQL versions
ii  postgresql-server-dev-10                   10.6-0ubuntu0.18.04.1       



sudo docker run -p 5432:5432 -e POSTGRES_USER=hoge -e POSTGRES_PASSWORD=hoge -d postgres:10
psql -d hoge -U hoge -h localhost

vi config/database.yml  

database: hoge
username: hoge
password: hoge
host: localhost

rails s
bin/rails db:migrate RAILS_ENV=development


vi 

 docker run -v /host/path:/container/path image-name

状態確認
sudo docker ps

docker永続化起動
sudo docker run -v volume-data:/container/path -p 5432 -e POSTGRES_USER=hoge -e POSTGRES_PASSWORD=hoge postgres:10

ボリューム割当
docker volume create database-data


git remote add origin https://github.com/karaage578/tweet_app.git


cd tweet_app
git init
git add .
git commit


20190209
datebase.ymlの編集

default: &default
  adapter: postgresql
  pool: 5
  username: hoge
  password: hoge
  host: localhost
development:
  <<: *default
  database: tweet_app_dev
  test:
  <<: *default
  database: tweet_app_test

production:
  <<: *default
  database: tweet_app_pro


Gemgfileでpgを指定
/home/takeda/git/tweet_app/Gemfile
gem 'sqllite3' ⇛ gem 'pg'

データベース作成コマンドを実行
https://qiita.com/windhorn/items/0f58866291f8273f18fb
  bundle exec rake db:create
  ※datebase.ymlを読み込んでdatebaseを作成する

takeda@takeda-FMVA56KWY:~/git/tweet_app$ rails g model Post content:text
マイグレートする
rails db:migrate
サーバーを立ち上げ直す
rails s
  https://qiita.com/pugiemonn/items/718b7360028286c5b626


