```uml
@startuml
[*]->メインページ
state メインページ{
state "rogin" <<sdlreceive>> 
state rogin
    [*]-> rogin : ログインアイコンをクリック
}


state ログイン{
state input <<choice>>
state "mainpage" as main <<sdlreceive>>
state main
入力画面:do/メールアドレス,パスワード入力
エラー:do/エラーを表示
    [*]-> 入力画面
    入力画面->input

    input -->エラー:メール or パスワードが違っていた場合
    input --> main:両方あっていた場合
}
@enduml
```