 
20190209レッスン
===
[やったこと](https://qiita.com/ynarasak/items/b9bb5b35f14ed6152134)
#### gitにプッシュ
```
git add .
git commit
git push origin master
```

#### sidekiqをinstall
[管理画面表示方法](https://qiita.com/yumiyon/items/6835d90e621e73268021)
Gemfile編集
```ruby
gem 'sidekiq'
```
[sidikiq.ymlを編集](https://dev.classmethod.jp/server-side/ruby-on-rails/ruby-on-rails_active-job-sidekiq/)
※自分で作成しないとないため、プロジェクトは以下のconfigでファイルを新規作成する
```yml
:concurrency: 25
:pidfile: ./tmp/pids/sidekiq.pid
:logfile: ./log/sidekiq.log
:queues:
  - default
```
#### redisをinstall
Gemfile編集
```ruby
gem 'redis', '~> 4.0'
```
[redis起動](https://qiita.com/iyuichi/items/3a6f748cf1069205ba46)
```
bundle install
sudo docker run --name redis -d -p 6379:6379 redis redis-server --appendonly yes
```

#### (ジョブの実行)[https://qiita.com/mktoho-n/items/d75c0b84943fb3543cd1]


####[IFTTT配信先](http://oita.oika.me/2017/09/16/ifttt-push-to-phone/)
``` 
https://maker.ifttt.com/trigger/test/with/key/bJQ3IaL-4wS7zs87PQ4J0N
```
```json
{
	"value1" : "a",
	"value2" : "b",
	"value3" : "http://localhost:3000/posts/index"
}
```

##　課題
+ job作成
+ [sidekiqでジョブスケジュール起動](ActiveJob, sidekiq, sidekiq-schedulerを使ってRailsで定期処理)
-　config/routes.rb編集後はrails sをし直す必要あり。

## 起動コマンド
cd /home/takeda/git/tweet_app/
sudo docker run -v volume-data:/var/lib/postgresql/data -p 5432:5432 -e POSTGRES_USER=hoge -e POSTGRES_PASSWORD=hoge postgres:10
rails s
bundle exec sidekiq -C config/sidekiq.yml
sudo docker run --name redis -d -p 6379:6379 redis redis-server --appendonly yes