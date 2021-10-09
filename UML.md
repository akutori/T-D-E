```uml
@startuml
title 画面遷移図
state "ログイン" as login <<sdlreceive>>
state "カート" as cart <<sdlreceive>>
state "商品詳細" as detail <<sdlreceive>>
state "トップページ" as main <<sdlreceive>>
state "登録完了" as completionofregistration <<sdlreceive>>
state "検索後画面" as search <<sdlreceive>>

[*]->main
main->ヘッダー


state ヘッダー{

}

state マイページ{
state "購入履歴" as bought <<sdlreceive>>
state "アイコン編集" as icon <<sdlreceive>>
state "登録内容変更" as change <<sdlreceive>>

[*]->bought : 購入履歴をクリック
[*]-->change : 「編集」をクリック
[*]->icon : プロフィールアイコンをクリック
}
@enduml
```