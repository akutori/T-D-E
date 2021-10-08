```uml
@startuml

[*]->トップページ
トップページ->ログイン
トップページ-->カート
トップページ-up->商品詳細

state トップページ<<mainpage>>{
state "ログイン" as maintologin <<sdlreceive>>
state "カート" as maintocart <<sdlreceive>>
state "商品詳細" as maintodetail <<sdlreceive>>
state "ヘッダー" as headder <<sdlreceive>>
    [*]-> maintologin :ログインアイコンをクリック
    [*]--> maintocart :カートをクリック
    [*]-up-> maintodetail :商品をクリック
    [*]-left-> headder :ヘッダー要素をクリック
}

state ログイン<<login>>{
state input <<choice>>
state "トップページ" as logintomain<<sdlreceive>>

入力画面:do/メールアドレス,パスワード入力
エラーページ:do/エラーを表示
    [*]--> 入力画面
    入力画面->input
    input->エラーページ:メール or パスワードが違っていた場合
    input-->logintomain : 両方あっていた場合

}

state 購入画面{
state "トップページ" as detailtomain<<sdlreceive>>
注文確定:do/注文を確定したことを表示する
    [*]->注文確定 :購入確定を押したとき
    注文確定-->detailtomain
}


state カート{
state "商品詳細" as carttodetail <<sdlreceive>>

    [*]->carttodetail :クリックする
}

state 商品詳細<<detail>>{
state "カート" as detailtocart <<sdlreceive>>

    [*]->detailtocart :カートに入れるをクリック
}

@enduml
```