```uml
@startuml
[*]->メインページ
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
エラー:do/エラーを表示
    [*]--> 入力画面
    入力画面->input
    input-->エラーページ:メール or パスワードが違っていた場合
    input-->mainpage : 両方あっていた場合

}

state 購入画面{
    [*]->注文確定 :購入確定を押したとき
}

state カート{
    [*]->goodsdetail :クリックする
}
state 商品詳細{
    [*]->cart :カートに入れるをクリック
}

@enduml
```