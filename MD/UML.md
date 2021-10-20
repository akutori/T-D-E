```uml
@startuml
scale 1.22
title 画面遷移図
state ifmain <<choice>>
state "トップページ" as main <<sdlreceive>>

[*]--> main
main -left-> ifmain : プロフィールアイコン\nをクリック
ifmain -up-> マイページ :ログイン時
ifmain -left->ログイン :未ログイン時
ログイン-->新規登録画面 :ログインはこちらをクリック
main->検索後画面
note top of 検索後画面
ヘッダーより
1,検索ボックスからの入力
2,poopularをクリック
3,カテゴリを選択
4,ハードを選択
5,もっと見るをクリック
のいずれかを行うことにより遷移します
end note

state ログイン{
    state iflogin <<choice>>
    state ログインエラー表示:画面の遷移はしない
    state "トップページ" as maininlogin <<sdlreceive>>

    [*]-> iflogin : ログイン情報入力
    iflogin -up-> ログインエラー表示 : 入力情報誤り
    ログインエラー表示 -up-> iflogin
    iflogin -> maininlogin : ログイン成功時
}

state 検索後画面{
state "商品詳細" as serchdetail <<sdlreceive>>
state 並べ替え :do/商品の並べ替えを行う
[*]-> serchdetail : 商品サムネイル\nor\n商品名をクリック
[*]--> 並べ替え 
並べ替え-up-> serchdetail :並べ替えを指定

}


state 商品詳細から購入完了{
    state if1 <<choice>>
    state if11 <<choice>>
    state "商品詳細" as detail1 <<sdlreceive>>
    state "カート" as cart1 <<sdlreceive>>
    state "支払画面" as cashregister1 <<sdlreceive>>
    state "カート内商品削除確認" as deletegodds <<sdlreceive>>
    state "カート内商品削除完了" as deleteafter <<sdlreceive>>
    state "購入後画面" as buyafter <<sdlreceive>>
    state "トップページ" as main1 <<sdlreceive>>
state "購入確認" as buycheck <<sdlreceive>>

    [*]-> detail1
    detail1 --> cart1 : カートに入れる\nをクリック
    cart1 -> if1
    if1 -up-> cashregister1 : 支払いに進むをクリック
cashregister1 -> buycheck : 支払うをクリック
    buycheck -> buyafter : 購入をクリック
    buyafter -up-> main
    
    if1 --> deletegodds : 削除をクリック
    deletegodds -> deleteafter : 削除をクリック
    deleteafter --> if11
    if11 -left-> main1 : TOPへをクリック
    if11 --> cart1 : カートへをクリック

}

state マイページ{
state "購入履歴" as bought <<sdlreceive>>
state "アイコン編集" as icon <<sdlreceive>>
state "登録内容編集" as change <<sdlreceive>>

[*]-up->bought : 購入履歴をクリック
[*]-->change : 「編集」をクリック
[*]->icon : プロフィールアイコン\nをクリック
}


state 新規登録画面{
state "登録確認" as checkregist <<sdlreceive>>
state "登録完了" as okregist <<sdlreceive>>
state "トップページ" as maininregist <<sdlreceive>>
'state "ログイン" as rogininregist <<sdlreceive>>
state 入力フォーム:入力フォーム

[*]->入力フォーム
入力フォーム->checkregist : 「登録」をクリック
入力フォーム -up-> ログイン : ログインはこちらをクリック
checkregist -> okregist : 入力情報に不足,ミス無し
okregist -> maininregist
checkregist -up-> 入力フォーム : 入力情報にミスあり
}
@enduml
```