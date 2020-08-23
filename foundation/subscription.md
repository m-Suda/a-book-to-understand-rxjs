# [WIP]Subscription

## What is this?
- ObserverがObservableに追加された結果のこと
- [WIP]Observableは自身を`.subscriber()`したObserverの情報をObservable自身に登録する。その登録した結果がSubscription
- Subscriptionで`.unsubscribe()`できる
