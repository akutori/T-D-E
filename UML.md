```uml
@startuml
[*]->メインページ
メインページ->ログイン
メインページ-->カート
メインページ-up->商品詳細

state メインページ{
state "rogin" <<sdlreceive>>
state "cart" <<sdlreceive>>
state "goodsdetail" <<sdlreceive>>
    [*]-> rogin :ログインアイコンをクリック
    [*]--> cart :カートをクリック
    [*]-up-> goodsdetail :カートをクリック
}

state ログイン{
state input <<choice>>
state "mainpage"<<sdlreceive>>

入力画面:do/メールアドレス,パスワード入力
エラーページ:do/エラーを表示
    [*]--> 入力画面
    入力画面->input
    input->エラーページ:メール or パスワードが違っていた場合
    input-->mainpage : 両方あっていた場合

}

state 購入画面{
state "メインページ" as returnmain<<sdlreceive>>
注文確定:do/注文を確定したことを表示する
    [*]->注文確定 :購入確定を押したとき
    注文確定-->returnmain
}


state カート{
state "goodsdetail" as goodsincart <<sdlreceive>>

    [*]->goodsincart :クリックする
}

state 商品詳細{
state "cart" as detailincart <<sdlreceive>>

    [*]->detailincart :カートに入れるをクリック
}

@enduml
```