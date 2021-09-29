```uml
@startuml




[*]->メインページ
メインページ->ログイン
メインページ-->カート
メインページ-up->商品詳細

state メインページ<<mainpage>>{
state "ログイン" as logininmainpage  <<sdlreceive>>
state "カート" as cartinmainpage <<sdlreceive>>
state "商品詳細" as goodsdetailinmainpage <<sdlreceive>>
    [*]-> logininmainpage :ログインアイコンをクリック
    [*]--> cartinmainpage :カートをクリック
    [*]-up-> goodsdetailinmainpage :カートをクリック
}

state ログイン<<login>>{
state input <<choice>>
state "メインページ" as mainpageinlogin<<sdlreceive>>

入力画面:do/メールアドレス,パスワード入力
エラーページ:do/エラーを表示
    [*]--> 入力画面
    入力画面->input
    input->エラーページ:メール or パスワードが違っていた場合
    input-->mainpageinlogin : 両方あっていた場合

}

state 購入画面{
state "メインページ" as mainpageingoodsdetail<<sdlreceive>>
注文確定:do/注文を確定したことを表示する
    [*]->注文確定 :購入確定を押したとき
    注文確定-->mainpageingoodsdetail
}


state カート{
state "商品詳細" as goodsdetailincart <<sdlreceive>>

    [*]->goodsdetailincart :クリックする
}

state 商品詳細{
state "カート" as cartingoodsdetail <<sdlreceive>>

    [*]->cartingoodsdetail :カートに入れるをクリック
}

' メインページカラー
skinparam stateBorderColor<<mainpage>> #40fff5
state メインページ #9efffa
state mainpageingoodsdetail #9efffa
state mainpageinlogin #9efffa

' ログインカラー
skinparam stateBorderColor<<login>> #ff73ff
state ログイン #ffd4ff
state logininmainpage #ffd4ff

@enduml
```