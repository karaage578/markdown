### [Modelについて](https://qiita.com/macotok/items/a17a4b0d22db4e885678)
------------------------------------------------
- モデル作成(マイグレーションファイルが作成される)
```
rails generate model モデル名(ex,User) カラム名:データ型(ex,name:string)
```
- マイグレーションファイルの適用(テーブルやカラムが作成される)
```
rails db:migrate
```

- [テーブル削除](https://qiita.com/kanuu/items/a9223712ee0ff8d19d56~)
```
rails generate migration クラス名
rails db:migrate
```
-----------------------
###### [マイグレーションファイルの記載](https://qiita.com/zaru/items/cde2c46b6126867a1a64)
- テーブル削除
```
drop_table :テーブル名
```
- テーブル名変更
```
rename_table :変更前テーブル名, :変更後テーブル名
```
- カラム追加
```
add_column :テーブル名 :カラム名 :データ型
```
-　カラム変更
```
change_column :テーブル名, :カラム名, :データ型,
```
- カラム削除
```
remove_column :テーブル名 :カラム名 :データ型
```
