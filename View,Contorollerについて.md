## View,Controllerについて
-----------------------------
##### [●renderメソッド](https://qiita.com/hayashino/items/c2a4e7d3edbdcce3cd2a)

---------------------------
### ●ヘッダーにページリンクを追加するとき
- application.html.erbのheader部分に追記
```html
<body>
    <header>
        <div>
            <%= link_to("タグ"), "リンク先" %>
        </div>
    </header>
</body>
```
### ●一覧ページ
- index_html.erb
```html
<!-- テーブルにあるすべての投稿内容を表示 -->
<% 変数名(posts).each do |モデル名(post)| %>
    <div>
        <%= モデル名(post).カラム名(content) %>
    </div>
<% end %>
```
- controller
```ruby
def index
    @変数名(posts) = モデル名(post).all
end
```
- route.rb
```ruby
get "コントローラー名/index" => "コントローラー名#index"
```
##### ●一覧ページの投稿の並び替え
- controller
```ruby
def
    @変数名 = モデル名.all.order(カラム名(created_at): :asc(昇順),desc(降順))
end
```
##### ●投稿詳細ページ(idは投稿作成時に必ず作成され、キーをして使用)
- index_html.erb
```html
    <% @変数.each do |モデル名| %>
      <div>
        <%= link_to(モデル名.投稿内容を格納するカラム名, "/コントローラー名/#{モデル名.id}") %>
        <!-- <%= link_to(タグ, "飛び先URL") %> 投稿n内容を押すとその詳細ページに飛ぶ用にする-->
      </div>
    <% end %>
```
- show_html.erb
```html
<!-- 投稿内容 + 詳細ページで表示したい内容を表示する -->
<div>
    <p>
        <% @変数名.投稿内容を格納するカラム名 %>
    </p>
</div>
<div>
    <p>
        <% @変数名.投稿日付や投稿者を格納するカラム %>
    </p>
</div>
```
- controller
```ruby
def show
    @変数名 = モデル名.find_by(id: params[:id])
end
```
- route.rb
```ruby
get "posts/:id" => "posts#show"
```
### ●データ登録ページ
- html.erb
```html
<%= form_tag("/コントローラー名/create") do %>
    <div>
        <textarea name="属性名"></textarea>
        <input type="submit" value="投稿">
    </div>
<% end %>
```
- controller
```ruby
def new
end

def create
   @変数名 = モデル名(Post).new(カラム名: params[:属性名])
   #カラムにデータ(params[])を挿入
   @変数名.save
   redirect_to("登録後の遷移先URL")
end
```
- route.rb
```ruby
get "コントローラー名/new" => "コントローラー名#new"
post "コントローラー名/create" => "コントローラー名#create"
```
##### ●データの編集、削除
- edit_html.erb
```html
    <%= form_tag("/posts/#{@post.id}/update") do %>
    <!-- form_tag(URL) do でフォーム内の内容を指定URLへPOSTする -->
      <div>
        <div>
          <textarea name="content"><%= @post.content %></textarea>
          <!-- <textarea>初期値</textarea> と囲むと初期値を設定できる -->
          <%= f.submit "保存", date: {conform: "保存してもいいですか？", disable_with: "処理中..."} %>
        </div>
      </div>
    <% end %>
```
- show_html.erb
```html
<div>
    <%= link_to("編集", "/コントローラー名/#{@変数名.id}/edit" %>
    <%= link_to("削除", "/コントローラー名/#{@変数名.id}/destroy", method: :delete data: { confirm: "削除しますか？" }) %>
    <!-- {method: "post"}によりpostのルーティングにマッチするようになる -->
</div>
```
- controller
```ruby
def edit
    @変数名 = モデル名.find_by(id: params[:id])
    # 特定のidのレコードを引っ張ってくる
end

def update
    @変数名 = モデル名.find_by(id: params[:id])
    # 特定のidのレコードを引っ張ってくる
    @変数名.content = params[:content]
    @変数名.save
    # カラムにコンテンツを保存
    redirect_to("保存後のリダイレクト先")
end

def delete
    @変数名 = モデル名.find_by(id: params[:id])
    @変数名.destroy
    # 特定のidのレコードを削除
    redirect_to("削除後のリダイレクト先")
end
```
- route.rb
```ruby
  get "コントローラー名/:id/edit" => "コントローラー名#edit"
  post "コントローラー名/:id/update" => "コントローラー名#update"
  resources :posts
```
- バリデーションの追加(modeles/モデル名.rb)
```ruby
class
    validates :content, {presence: true}
end
```
----
##ユーザー作成・編集・削除機能

#### Userモデル、usersテーブルの作成
```
rails generate model User user_id:string email:string
rails db:migrate
```
#### ユーザーデータの登録
```
rails c
user = User.new(user_id: "test", email: "karaage118@gmail.com")
user.save
``` 
#### バリデーション追加
models/user.rb
```rubu
validates :name, {presence: true}
validates :email, {uniquness: true}
```
#### ユーザー一覧、詳細、編集ページの作成
- コントローラーの作成
```
rails generate controller users index
```
- View,Controllerはほぼ投稿ページ作成と同じ

## ログイン・ログアウト機能
-　ログインページ作成
```html
<%= form_tag("/login") do %>
    <p>メールアドレス</p>
        <input name="email" value="<%= @email %>">
    <p>パスワード</p>
        <input type="password" name="password" value="<%= @password %>">
        <input type="submit" value="ログイン">
<% end %>
```
- passwordカラムの追加
```
rails g migration addpassword_to_users
```
```ruby
def
    add_column :users, :password, :string
end
```
```
rails db:migrate
```
- コントローラー
```ruby
def login_form
end

def login
  @user = User.find_by(email: params[:email], password: params[:password])
  if @user
    session[:user_id] = @user.id
    flash[:notice] = "ログインしました"
    redirect_to("/posts/index")
  else
    @error_message = "メールアドレスまたはパスワードが間違っています"
    @email = params[:email]
    @password = params[:password]
    render("users/login_form")
  end
end

def logout
  session[:user_id] = nil
  flash[:notice] = "ログアウトしました"
  redirect_to("/login")
end
```
- ルーティングの追加
```ruby
get "login" => "users#login_form"
post "login" => "users#login"
post "logout" => "users#logout"
```
-
```
```
-
```
```
-
```
```
#### 
