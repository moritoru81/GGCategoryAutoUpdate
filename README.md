GrepGrep Category Auto Update Plugin
=====================================

このプラグインは，記事投稿時におけるカテゴリーの自動更新をサポートします。
XMLRPCリクエストや通常に投稿において，投稿記事内に決められた記述形式でカテゴリー指定を書いておくことで，投稿記事のカテゴリーを指定されて内容で更新します。

Version
-------

* 0.1-beta


動作環境
-------

* WordPress 3.5.1（テスト確認済み）
* PHP5.3以上

インストール
----------

以下にプラグインファイルを展開し，管理画面より有効化してください。

    <wordpress>/wp-content/plugins

マニュアル
--------

### カテゴリーの指定

カテゴリーの指定は以下の方法で行ないます。

#### 階層指定

「>」が階層区切り文字になります。以下では，cat1がcat2の親，cat2がcat3の親であり，記事はカテゴリーcat3に属します。

    <!-- ggcat[cat1>cat2>cat3] -->

#### 複数指定

カンマ，半角または全角スペースが区切り文字になります。以下では，記事がcat1かつcat2かつcat3の３つのカテゴリーに属します。

    <!-- ggcat[cat1,cat2,cat3] -->
    <!-- ggcat[cat1 cat2 cat3] -->
    <!-- ggcat[cat1　cat2　cat3] -->
    
**その他注意事項**

* catには，カテゴリーID・カテゴリー名・スラッグのいずれかを指定可能です。階層指定と複数指定を混合させることはできません。
* 上記の指定は，投稿記事内のいずれの場所であっても可能です。エスケープされた場合はその限りではありません。
* カテゴリー指定が投稿記事内に複数存在した場合，最初に見つけられる指定が有効です。
* カテゴリー指定は，途中で改行した場合は無効です。

### プラグイン設定

設定は，管理画面 > 設定 > GGCategoryAutoUpdate で変更可能です。

* デフォルトカテゴリ
    * 投稿がこのカテゴリーである場合にカテゴリーが「未分類」と判断します。複数存在する場合は，カンマ区切りで指定します。「*」を指定するとすべてのカテゴリーに対して適用されます。
* すべての投稿に適用
	* 通常は，XMLRPCリクエストのみに適用されます。「すべての投稿に適用」を選択すると，XMLPRC以外の投稿にも適用されます。
* 更新後の構文削除
	* 更新後に投稿記事内のカテゴリー構文を削除するかどうかを制御します。
* カテゴリーが存在しない場合の動作
	* 「新規に作成する」を選択した場合，カテゴリー編集権限があれば新規にカテゴリーが作成されます。作成されるカテゴリーは，指定されたカテゴリーを「カテゴリー名」として作成します。
* 対象の投稿タイプ
	* プラグインを適用する投稿タイプを指定します。通常は，「post」のみを想定していますが，カスタム投稿タイプを作成しプラグインを適用したい場合はここに追記します。複数存在する場合は，カンマ区切りで指定します。
* カテゴリー指定構文
	* この正規表現のサブパターンで指定される内容を「カテゴリー指定」として判断します。サブパターンは必ず１つ含まれる必要があります。

WP Options
----------

以下のオプション名でwp_optionsを利用します。

    GGCategoryAutoUpdate

DEBUG
------

以下の定数をtrueに設定することで，プラグインディレクトリ内のファイルにデバッグメッセージを出力します。

    define('GG_CATEGORY_AUTO_UPDATE_DEBUG', true);