```uml

@startuml
'defineによるカラー変数の設定
scale 2
!define MASTERCOLOR #fc8403
!define TABLECOLOR #59b7ff

entity "**goods**\n商品" as goods<<マ,MASTERCOLOR>> {
    + 商品ID **[PK]**
    --
    商品名
    商品画像
    商品値段
    商品ゲーム種別
    ハードID**[FK]**
    在庫数
    商品内容
    ダウンロード商品
    商品発売日
    商品人気度
    削除フラグ
    クロスプレイ対応フラグ
}

'entity "**quantity**\n在庫テーブル" as quantitity<<テ,'TABLECOLOR>>{
'    + 商品ID**[PK]**
'    --
'    商品在庫数
'}

entity "**video**\n動画テーブル" as video<<テ,TABLECOLOR>>{
    + 商品ID**[PK][FK]**
    --
    動画URL
}
entity "**hard**\nハードテーブル" as hard<<テ,TABLECOLOR>>{
    + ハードID **[PK]**
    --
    ハード組み合わせ名
}

note left of hard
ハードの組み合わせを予め作っておきます。
例：001 = ps4
　　010 = PC
　　100 = switch
　　011 = ps4,PC
end note

entity "**user**\nユーザー" as user <<マ,MASTERCOLOR>>{
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
    entity "**ph**\n購入履歴テーブル" as ph <<テ,TABLECOLOR>>{
        + 購入履歴ID**[PK]**
        --
        - ユーザーID **[FK]**
        - 商品ID **[FK]**
        購入日
    }
    entity "**cart**\nカートテーブル" as cart <<テ,TABLECOLOR>>{
        - 商品ID **[PK][FK]**
        - ユーザーID **[PK][FK]**
    }

    note right of cart
        意図的に同じ商品を一度に購入
        できないようにしています。
    end note

'goods ||-|| quantitity
goods ||-u-|| video
goods ||-l-|| hard
user ||-u-o{ cart
goods ||-d-o{ ph
user ||-l-o| ph
goods ||-o{ cart
@enduml
```