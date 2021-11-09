```uml
@startuml
'defineによるカラー変数の設定
scale 2
!define MASTERCOLOR #fc8403
!define TABLECOLOR #59b7ff

entity "**ph header**\n購入履歴ヘッダー" as phheader <<テ,TABLECOLOR>>{
    + 購入履歴ID**[PK]**
    --
    - ユーザID**[FK]**
    - 商品ID**[FK]**
    個数
    '値段
    購入日時
    支払方法
    小計
    'お預かり額
    'お釣り 
}

entity "**goods**\n商品" as goods<<マ,MASTERCOLOR>> {
    + 商品ID **[PK]**
    --
    - ハードID**[FK]**
    - ゲームID**[FK]**
    在庫数
    商品内容
    ダウンロード商品
    商品発売日
    商品人気度
    
    削除フラグ 
}

entity "**game**\nゲームテーブル" as game<<テ,TABLECOLOR>>{
    + ゲームID**[PK]**
    --
    - ジャンルID**[FK]**
    ゲーム名
    値段
    クロスプレイ対応フラグ
}

entity "**category**\nゲームカテゴリーテーブル" as category<<テ,TABLECOLOR>>{
    + カテゴリーID**[PK]**
    --
    - ゲームID**[FK]**
}

entity "**download**\nダウンロード商品可否テーブル" as download<<テ,TABLECOLOR>>{
    + ゲームID**[PK]**
    --
    - ダウンロード商品フラグ
}

'entity "**quantity**\n在庫テーブル" as quantitity<<テ,'TABLECOLOR>>{
'    + 商品ID**[PK]**
'    --
'    商品在庫数
'}

entity "**video**\n動画テーブル" as video<<テ,TABLECOLOR>>{
    - 商品ID**[PK][FK]**
    --
    動画URL
}
entity "**hard**\nハードテーブル" as hard<<テ,TABLECOLOR>>{
    + ハードID **[PK]**
    --
    ハード名
}

'note left of hard
'ハードの組み合わせを予め作っておきます。
'例：001 = ps4
'　　010 = PC
'　　100 = switch
'　　011 = ps4,PC
'end note

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

    entity "**ph**\n購入履歴テーブル" as ph <<テ,TABLECOLOR>> {
        - 購入履歴ID**[FK]**
        --
        - 商品ID **[FK]**
        行番号
        商品名
        個数
        値段
    }

    note left of ph
        行番号は同じ購入履歴IDの商品を
        羅列したものに番号を割り当てただけです。    
    end note

    entity "**cart**\nカートテーブル" as cart <<テ,TABLECOLOR>>{
        - 商品ID **[FK]**
        - ユーザーID **[PK][FK]**
        --
        個数
    }

    note top of cart
        意図的に同じ商品を一度に購入
        できないようにしています。
    end note

'goods ||-|| quantitity
goods ||-u-|| video
goods ||-l-|| hard
user ||-u-o{ cart
goods ||-d-o{ ph
'ユーザーからみて自分のユーザーIDは0以上存在する
goods ||-o{ cart
user ||-l-o{ phheader
phheader ||-l-|{ ph
goods ||--o{ phheader
@enduml
```