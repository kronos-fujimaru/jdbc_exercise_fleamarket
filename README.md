# JDBC演習 フリマアプリ開発

## 処理概要

コンソール画面で動作するフリマアプリを作成します。次のプロジェクト（Zipファイル）をインポートして開発を進めてください。

[演習用プロジェクト](./src/fleamarket-db.zip)

> Eclipseでのインポート手順<br>①インポート -> フォルダまたはアーカイブからプロジェクト -> [アーカイブ]ボタン -> Zipファイルを選択<br>②フォルダーのリスト内の一番上にある「fleamarket-db.zip_expanded」のチェックを外して[完了]ボタンをクリック

<br>

画面レイアウトなどのベースとなるコードやログイン機能、DTOクラス（Itemクラスなど）は実装済みです。MainクラスやDAOクラスを修正し、以下の機能を実装してください。

<br>

**1. ログイン機能**　※実装済み
```
**********************
**  みんなのフリマ  **
**********************
【ログイン】
メールアドレス：ohagi@example.com
パスワード：ohagi

ようこそ！おはぎさん
```

<br>

**2. 商品一覧表示**　※実装済み
```
【商品一覧】
  ID | 商品名                                             |     価格 | 状態 |                 更新日 |
-----------------------------------------------------------------------------------------------------
   1 | ノートPC KroBook メモリ32GB SSD512GB               |   200000 | A    |  2022-05-10 10:18:32.0 |
   2 | 実践SQL                                            |     1200 | D    |  2022-06-05 14:23:09.0 |
   3 | レンズ 一眼レフカメラ用 50mm F1.4                  |    45000 | A    |  2022-05-15 07:03:54.0 |
   4 | 黒いタブレット SIMフリー 64GB                      |    32000 | B    |  2022-05-19 11:32:11.0 |
   5 | タブレット 9.7インチ シリコンケース                |     3800 | S    |  2022-05-19 16:51:10.0 |
   6 | Javaプログラミング入門 第3版                       |     2800 | B    |  2022-06-10 14:09:49.0 |
   7 | 黒い粉                                             |      300 | S    |  2022-05-25 17:12:44.0 |
   8 | 受講者Xの健診                                      |      900 | A    |  2022-05-30 12:45:37.0 |
   9 | 消せるボールペン                                   |      300 | S    |  2022-06-04 09:51:56.0 |
  10 | ミラーレス一眼カメラ K02X                          |    98000 | A    |  2022-06-08 19:20:54.0 |
  11 | 新！Javaのすべてがわかる本                         |     1500 | C    |  2022-06-08 22:07:08.0 |
  12 | プレミアム万年筆                                   |     5000 | S    |  2022-06-09 15:43:11.0 |
  13 | なぜSQLが使われるのか 第12版                       |     4000 | S    |  2022-06-10 08:12:59.0 |
  14 | ノートパソコン SiroBook メモリ32GB SSD256GB        |   128000 | B    |  2022-06-15 10:50:38.0 |
  15 | MySQL 8.0 マスター                                 |      800 | E    |  2022-06-15 16:20:19.0 |

***** メニュー *****
1:検索　2:出品　3:更新　4:削除　9:ログアウト
```

<br>

**3. 検索機能（商品名による部分一致検索）**
```
***** メニュー *****
1:検索　2:出品　3:更新　4:削除　9:ログアウト
1

-----------------------------------------------
検索キーワードで商品名の部分一致検索をします。
※未入力の場合は全件検索します。
-----------------------------------------------
検索キーワード：java

【商品一覧】
  ID | 商品名                                             |     価格 | 状態 |                 更新日 |
-----------------------------------------------------------------------------------------------------
   6 | Javaプログラミング入門 第3版                       |     2800 | B    |  2022-06-10 14:09:49.0 |
  11 | 新！Javaのすべてがわかる本                         |     1500 | C    |  2022-06-08 22:07:08.0 |
```

<br>

**4. 出品機能（商品登録機能）**

```
***** メニュー *****
1:検索　2:出品　3:更新　4:削除　9:ログアウト
2

【出品】
------ 出品する商品情報を入力してください ------
商品名：JDBCのコツが何となくわかる本
価格：2500
状態：A

商品を登録しました。

（商品一覧表示）
```

<br>

**5. 商品更新機能**

※更新内容はすべて入力される想定

```
***** メニュー *****
1:検索　2:出品　3:更新　4:削除　9:ログアウト
3

【商品更新】
------ 更新するIDを入力してください ------
ID：16

------ 更新内容を入力してください --------
商品名：JDBCのコツが何となくわかる本
価格：2000
状態：B

商品を更新しました。

（商品一覧表示）
```

指定したIDが存在しない場合

```
***** メニュー *****
1:検索　2:出品　3:更新　4:削除　9:ログアウト
3

【商品更新】
------ 更新するIDを入力してください ------
ID：999

指定したIDの商品は見つかりません

（商品一覧表示）
```

<br>

**6. 商品削除機能**

```
***** メニュー *****
1:検索　2:出品　3:更新　4:削除　9:ログアウト
4

【商品削除】
------ 削除するIDを入力してください ------
ID：16

商品を削除しました。

（在庫一覧表示）
```

指定したIDが存在しない場合

```
***** メニュー *****
1:検索　2:出品　3:更新　4:削除　9:ログアウト
4

【商品削除】
------ 削除するIDを入力してください ------
ID：999

指定したIDの商品は見つかりません。

（在庫一覧表示）
```

<br>

**7. ログアウト機能**　※実装済み

```
***** メニュー *****
1:検索　2:出品　3:更新　4:削除　9:ログアウト
9

ログアウトしました。
```

<br>

## システム構成

**テーブル定義**

下記リンクのSQL演習を参照してください。**演習5**まで進めることでテーブルと初期データを用意できます。

[SQL演習](https://github.com/learning-kronos/sql-exercise)

> 別タブで開きたい場合はCtrlキーを押しながらクリックしてください。

<br>

**ItemDao.java（パッケージ：jp.kronos.dao）**

| 可視性 | メソッド名 | 戻り値 | 引数 | 説明 |
|-------|------------|-------|------|---------|
| public | findAll  | List\<Item>    | なし | 商品データを全件取得する。 |
| public | findByKeyword  | List\<Item>    | なし | 商品名による部分一致検索で商品データを取得する。 |
| public | findById | Item | int | 引数のIDに紐付く商品データを取得する。<br>データが存在しない場合は戻り値としてNullを返す。 |
| public | create   | なし | Item | 引数のItemクラスをもとに商品データを登録する。 |
| public | update   | なし | Item | 引数のItemクラスをもとに商品データを更新する。 |
| public | delete   | なし | int | 引数のIDに紐づく商品データを削除する。 |

> ソースコード内のコメントの「TODO」をもとに修正してください。

<br>

**UserMain.java（パッケージ：jp.kronos.main）**

| メソッド名 | 戻り値 | 引数 | 説明 |
|------------|-------|------|---------|
| login  | なし | なし | ログイン機能 |
| showItems  | なし | keyword | 商品一覧表示 / 検索機能 |
| create | なし | なし | 出品処理（商品登録処理） |
| update   | なし | なし | 商品更新処理 |
| delete   | なし | なし | 商品削除処理 |
| main   | なし | String[] | 入力されたメニューにより処理を分ける |

> ソースコード内のコメントの「TODO」をもとに修正してください。

<!-- [解答例](./ans/answer.md) -->
