```uml
@startuml
title 画面遷移図
state ifmain <<choice>>
state "ログイン" as login <<sdlreceive>>
state "カート" as cart <<sdlreceive>>
state "商品詳細" as detail <<sdlreceive>>
state "トップページ" as main <<sdlreceive>>
state "登録完了" as completionofregistration <<sdlreceive>>
state "検索後画面" as search <<sdlreceive>>
state "ヘッダー" as headder <<sdlreceive>>



[*]-->main
[*]->headder
headder->main : サイトロゴをクリック
main -> ifmain
ifmain -> マイページ
ifmain --> ログイン

state ヘッダー{
    state "ログイン" as logininheadder <<sdlreceive>>
    state ifheadder <<choice>>
    state ifheadder1 <<choice>>
    state "検索後画面" as searchinheadder <<sdlreceive>>
    [*]->ifheadder : プロフィールアイコンをクリック
    ifheadder->logininheadder : 未ログイン時
    ifheadder-up->マイページ : ログイン時
    [*]-->searchinheadder :ポピュラー,検索ボタンをクリック
    [*]-right->ifheadder1 : カテゴリ,ハードをクリック
    ifheadder1 -> searchinheadder : 項目をクリック
}

state ログイン{
    state iflogin <<choice>>
    state ログインエラー表示

    [*]-> iflogin : ログイン情報入力
    iflogin -up-> ログインエラー表示 : 入力情報誤り
    ログインエラー表示 -up-> iflogin
    iflogin -up-> main : ログイン成功時
}
state 商品詳細から購入完了{
    state if1 <<choice>>
    state if11 <<choice>>
    state "商品詳細" as detail1 <<sdlreceive>>
    state "カート" as cart1 <<sdlreceive>>
    state "支払画面" as cashregister1 <<sdlreceive>>
    state "購入後画面" as completion1 <<sdlreceive>>
    state "カート内商品削除確認" as deletegodds <<sdlreceive>>
    state "カート内商品削除完了" as deleteafter <<sdlreceive>>
    state "購入後画面" as buyafter <<sdlreceive>>
    state "トップページに" as main1 <<sdlreceive>>

    [*]-> detail1
    detail1 -> cart1 : カートに入れるをクリック
    cart1 -> if1
    if1 -> cashregister1 : 支払いに進むをクリック
    cashregister1 -> buyafter : 支払うをクリック
    buyafter -> [*]
    if1 --> deletegodds : 削除をクリック
    deletegodds -> deleteafter : 削除をクリック
    deleteafter --> if11
    if11 --> main1 : TOPへをクリック
    if11 --> cart1 : カートへをクリック

}

state マイページ{
state "購入履歴" as bought <<sdlreceive>>
state "アイコン編集" as icon <<sdlreceive>>
state "登録内容変更" as change <<sdlreceive>>

[*]->bought : 購入履歴をクリック
[*]-->change : 「編集」をクリック
[*]->icon : プロフィールアイコンをクリック
}
@enduml
```