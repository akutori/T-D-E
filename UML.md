```uml
@startuml




[*]->メインページ
メインページ->ログイン
メインページ-->カート
メインページ-up->商品詳細

state メインページ{
state "ログイン" as rogininmainpage  <<sdlreceive>>
state "カート" as cartinmainpage <<sdlreceive>>
state "商品詳細" as goodsdetailinmainpage <<sdlreceive>>
    [*]-> rogininmainpage :ログインアイコンをクリック
    [*]--> cartinmainpage :カートをクリック
    [*]-up-> goodsdetailinmainpage :カートをクリック
}

state ログイン{
state input <<choice>>
state "メインページ" as mainpageinrogin<<sdlreceive>>

入力画面:do/メールアドレス,パスワード入力
エラーページ:do/エラーを表示
    [*]--> 入力画面
    入力画面->input
    input->エラーページ:メール or パスワードが違っていた場合
    input-->mainpageinrogin : 両方あっていた場合

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

state メインページ #9efffa
state mainpageingoodsdetail #9efffa
state mainpageinrogin #9efffa

state ログイン #ffd4ff
state rogininmainpage #ffd4ff

@enduml
```