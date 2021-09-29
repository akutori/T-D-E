```uml
@startuml
state "rogin" <<sdlreceive>>
state input <<choice>>


[*]->メインページ
state メインページ{
    [*]--> rogin : ログインアイコンをクリック
    rogin -> [*]

}
state "rogin" <<sdlreceive>> 
state input <<choice>>
rogin -> ログイン
state ログイン{
    [*]-> 入力画面:do/メールアドレス,パスワード入力
    入力画面-->input
    input --> エラー:メールorパスワードが違っていた場合
    input --> トップページ:両方あっていた場合
}



@enduml
```