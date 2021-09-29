```uml
@startuml
[*] --> rogin:ログインするをクリック

[*] -> rogin

state rogin{
    [*]-> 入力画面:メールとパスワードを入力
}



@enduml
```