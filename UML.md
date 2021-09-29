```uml
@startuml

state input <<choice>>


[*]->メインページ
state メインページ{
state rogin
    [*]-> rogin : ログインアイコンをクリック

}
state "rogin" <<sdlreceive>> 

state ログイン{
state input <<choice>>
    [*]-> 入力画面:do/メールアドレス,パスワード入力
    入力画面->input
    input --> エラー:メールorパスワードが違っていた場合
    input --> トップページ:両方あっていた場合
}



@enduml
```