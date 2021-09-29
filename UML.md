```uml
@startuml
[*]->メインページ
state メインページ{
state rogin
    [*]-> rogin : ログインアイコンをクリック
}
state "rogin" <<sdlreceive>> 

state ログイン{
state input <<choice>>
state "mainpage" <<sdlreceive>>
入力画面:do/メールアドレス,パスワード入力
エラー:do/エラーを表示
    [*]-> 入力画面
    入力画面->input
    input --> エラー
    input -->エラー:メール or パスワードが違っていた場合
    input --> mainpage:両方あっていた場合
    input --> mainpage
}
@enduml
```