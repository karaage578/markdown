## Rails基礎知識
##### サーバーの起動
```
rails s
```
##### ●コンソールの立ち上げ
```
rails c
```
##### ●プロジェクトの作成
```
rails new アプリケーション名
```
##### ●最初のページの作成
- View,Controllerの作成
    - /app/view/コントローラー名/アクション名.html.erb
    - /app/controller/コントローラー名_controller.rb を作成
    ```
    rails g controller コントラローラー名 アクション名
    ```
    - controllerにアクションを作成
    ```ruby
    def アクション名
    end
    ```
    - routingの作成
    ```ruby
    get "URL" => "コントローラー名#アクション名"
    ```
##### ●新しいページの追加
- 同じコントローラーがある場合
    - /app/view/コントローラー名　配下に新アクション名_html.erbを作成
    - controllerにアクションを追加
    ```ruby
    def 新アクション名
    end
    ```
- コントローラーが未作成の場合
    - View,Controllerを作成
    ```
    rails g controller 新コントラローラー名 新アクション名
    ```
    - controllerにアクションを作成
    ```ruby
    def アクション名
    end
    ```

- routingの追加
    ```ruby
    get "URL" => "コントローラー名#アクション名"
    ```
--------------
##### ●テンプレート変数(htmlに埋め込んで使える変数)
.controller
```ruby
def
    @変数名 = "ほげほげ"
end
```
html.erb
```html
<%= @変数名 %>
```
##### ●リンクの作り方
 ルーティングのURL部分と同じにする
```html
<%= link_to(タグ, "飛び先URL") %>
```
```ruby
get "/" = "home#top"
```
##### ●フォームの作成
フォーム内の内容を指定のURLへPOSTする(デフォルトメソッドはPOST)
```ruby
form_tag(URL) do
end
```
##### ●保存前のアラート
```ruby
<%= f.submit "保存", date: {conform: "保存してもいいですか？", disable_with: "処理中..."} %>
```
##### ●削除時のアラート
```
<%= link_to 'Destroy', path, method: :delete, data: { confirm: '削除しますか？' } %>
```
##### ●gemのバーションの確認
```
bundle list
```
------------
# データの見方
- データの検索
```
rails c
モデル名.カラム名　#ex,user.name usersテーブルのnameカラムを表示
モデル名.find(id)　#id行目のレコードを表示
モデル名.find(カラム名: データ)　#カラムの項目がデータのレコードを表示
モデル名.all　#すべてのレコードを表示
```
- データの更新
```
>> user           # Just a reminder about our user's attributes
=> #<User id: 1, name: "Michael Hartl", email: "mhartl@example.com",
created_at: "2014-07-24 00:57:46", updated_at: "2014-07-24 00:57:46">
>> user.email = "mhartl@example.net"
=> "mhartl@example.net"
>> user.save
=> true
```
```
>> user.update_attribute(:name, "The Dude")
=> true
>> user.name
=> "The Dude"
```