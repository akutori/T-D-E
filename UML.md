```uml
@startuml
[*]->メインページ
state メインページ{
    [*]--> rogin : ログインアイコンをクリック

}
state "rogin" <<sdlreceive>> /* 定義済み処理 */
state input <<choice>>

state ログイン{
    [*]-> 入力画面:do/メールアドレス,パスワード入力
    入力画面-->input
    input --> エラー:メールorパスワードが違っていた場合
    input --> トップページ:両方あっていた場合
}



@enduml
```