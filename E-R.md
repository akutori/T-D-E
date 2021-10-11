```uml
@startuml
scale 2
'defineによるカラー変数の設定
!define MASTERCOLOR #fc8403
!define TABLECOLOR #59b7ff
entity "**goods**\n商品マスタ" as goods<<マ,MASTERCOLOR>> {
+ 商品ID **[PK]**
--
商品名
商品画像
商品値段
商品ゲーム種別
商品対応ハード
商品在庫(物理)
商品内容
ダウンロード商品
商品発売日
商品人気度
削除フラグ
}
entity "**user**\nユーザーマスタ" as user <<マ,MASTERCOLOR>>{
+ ユーザーID **[PK]**
--
ユーザ名
メールアドレス
パスワード
性別
郵便番号
住所
ユーザーサムネイル
}
package "ユーザーごとに持つ" as inunser{
    entity "**ph**\n購入履歴テーブル" as ph <<テ,TABLECOLOR>>{
        - ユーザーID **[PK][FK]**
        - 商品ID **[PK][FK]**
        --
        購入日
    }
    entity "**cart**\nカートテーブル" as cart <<テ,TABLECOLOR>>{
        - 商品ID **[PK][FK]**
        - ユーザーID **[PK][FK]**
        --
        個数
        削除フラグ
    }
}

user ||-u-|| cart
goods }o-d-|| ph
user ||-u-|| ph
goods }o---|{ cart
@enduml
```