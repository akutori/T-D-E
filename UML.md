```uml
@startuml
[*]->メインページ
state メインページ{
    [*]--> choice : ログインアイコンをクリック
    choice -->ログイン : ログインアイコンをクリック 
    ログイン:ログインボタンをクリック

}
state input <<choice>>
[*] -> ログイン

state ログイン{
    [*]-> 入力画面:メールとパスワードを入力
}



@enduml
```