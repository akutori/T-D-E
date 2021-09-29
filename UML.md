```uml
@startuml
[*]->メインページ
state メインページ{
    [*]--> choice
    choice -->ログイン : ログインアイコンをクリック 
    ログイン:ログインボタンをクリック

}

[*] -> ログイン

state ログイン{
    [*]-> 入力画面:メールとパスワードを入力
}

state input <<choice>>

@enduml
```