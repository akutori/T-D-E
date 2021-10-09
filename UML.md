```uml
@startuml
title 画面遷移図
state "ログイン" as login <<sdlreceive>>
state "カート" as cart <<sdlreceive>>
state "商品詳細" as detail <<sdlreceive>>
state "トップページ" as main <<sdlreceive>>
state "登録完了" as completionofregistration <<sdlreceive>>
state "検索後画面" as search <<sdlreceive>>
state "ヘッダー" as headder <<sdlreceive>>



[*]-->main
[*]-up->headder
headder->main : サイトロゴをクリック

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
    state ifjoin <<join>>
    state ログインエラー表示
    [*]--> iflogin : ログイン情報入力
    iflogin -> ログインエラー表示 : 入力情報誤り
    iflogin --> main
}
state 商品詳細から購入完了{
    state "商品詳細" as detail1 <<sdlreceive>>
    state "カート" as cart1 <<sdlreceive>>
    state "支払画面" as cashregister1 <<sdlreceive>>
    state "購入後画面" as completion1 <<sdlreceive>>
    [*]->

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