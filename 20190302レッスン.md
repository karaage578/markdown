 
20190302レッスン
===
##sidekiqをherokuで動作させる

#### Procfile編集
project内にProcfile作成

```
web: bundle exec rails server -p $PORT
worker: bundle exec sidekiq -C config/sidekiq.yml
```
#### redisのherokuアドオンを追加

#### git 過去commitに戻す

```
 git log --oneline
 git checkout 2d74c3b -- .
 git stash
```


##　課題
- webdyno:rails立ち上げ
- workerdyno:sidekiqとredisを立ち上げ
- 自動立ち上げのためにProcfileを記載する必要あり（workerdynoを立ち上げる必要があるため）
記載例
```
web: lein run -m myapp.web
worker: lein run -m myapp.worker 
```



