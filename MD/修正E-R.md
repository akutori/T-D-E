```uml
@startuml
'defineによるカラー変数の設定
scale 1.7
!define MASTERCOLOR #fc8403
!define TABLECOLOR #59b7ff

entity "**ph header**\n購入履歴ヘッダー" as phheader <<テ,TABLECOLOR>>{
    + 購入履歴ID**[PK]**
    --
    - ユーザID**[FK]**
    '- 商品ID**[FK]**
    --
    個数
    購入日時
    支払方法
    小計
    'お預かり額
    'お釣り
    '値段
}

entity "**goods**\n商品" as goods<<マ,MASTERCOLOR>> {
    + 商品ID **[PK]**
    --
    - ハードID**[FK]**
    - ゲームID**[FK]**
    - 在庫数**[FK]**
    - 動画URL**[FK]**
    - 人気度**[FK]**
    - 画像名**[FK]**
    --
    値段
    商品発売日
    ダウンロード商品フラグ
    削除フラグ 
}

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
        - 商品ID **[FK]**
        --
        行番号
        '商品名
        '個数
        値段
    }



    note top of ph
        行番号は同じ購入履歴IDの商品を
        羅列したものに番号を割り当てただけです。    
    end note

    entity "**cart**\nカートテーブル" as cart <<テ,TABLECOLOR>>{
        - 商品ID **[FK]**
        - ユーザーID **[PK][FK]**
        --
        個数
    }



package グッズ参照先 as pack{
        entity "**video**\n動画テーブル" as video<<テ,TABLECOLOR>>{
        + 商品動画ID**[PK]**
        --
        動画URL
    }

    entity "**hard**\nハードテーブル" as hard<<テ,TABLECOLOR>>{
        + ハードID **[PK]**
        --
        ハード名
    }

    entity "**genre**\nゲームジャンルーテーブル" as genre<<テ,TABLECOLOR>>{
        + ジャンルID**[PK]**
        --
        ジャンル名
    }

    entity "**game**\nゲームテーブル" as game<<テ,TABLECOLOR>>{
        + ゲームID**[PK]**
        --
        - ジャンルID**[FK]**
        - 画像ID**[FK]**
        --
        ゲーム名
        商品内容
        クロスプレイ対応フラグ
    }

    entity "**gameimage**\nパッケージ画像テーブル" as gameimage<<テ,TABLECOLOR>>{
        + ゲーム画像ID**[PK]**
        --
        画像名
    }

    entity "**quantity**\n在庫テーブル" as quantity<<テ,TABLECOLOR>>{
        + 在庫商品ID**[PK]**
        --
        在庫数
    }

    entity "**popular**\n人気度テーブル" as popular <<テ,TABLECOLOR>> {
        + 人気度商品ID **[PK]**
        --
        人気度
    }
    

}
note top of cart
    意図的に同じ商品を一度に購
    入できないようにしています。
end note

note top of pack
　商品とカーディナリティ(多重度)が
  同じのものをまとめました。
end note

goods }|-u-|| hard
goods ||-u-|| video
user ||-u-o{ cart
goods ||-d-o{ ph
goods ||-l-o{ cart
user ||-r-o{ phheader
phheader ||-r-|{ ph
goods ||--o{ phheader
goods ||-u-|| quantity
game }o-u-|| genre
game ||-u-|| gameimage
goods||-u-|| popular
goods }|-u--|| game

@enduml
```