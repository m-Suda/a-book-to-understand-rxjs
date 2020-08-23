# Observer

## What is this?
Observerは「Observableを`subscribe()`し、流れてくる値を受け取る側」のことだ。  
このObserverには`.next()`, `.error()`, `.complete()`の3つのメソッドを持ち、これらはそれぞれSubscription Functionで定義された同メソッドが呼ばれた時にそれぞれに対応するメソッドで値を受け取って処理をする。すなわちSubscription Functionからの通知をハンドリングするオブジェクトと呼べる。

## ソースコードで見てみよう
```typescript

const subscriptionFunction = observer => {
    observer.next(1);
    observer.next(2);
    observer.next(3);
    observer.complete();
};
const observable$ = Observable(subscriptionFunction);

const observer = {
    next: v => console.log(v),
    error: error => console.error(error),
    complete: () => console.log('Complete.')
}
observable$.subscribe(observer);
// 1
// 2
// 3
// Complete.

// または

observable$.subscribe(
    v => console.log(v),
    error => console.error(error),
    () => console.log('Complete.')
);
// 1
// 2
// 3
// Complete.
```
上記の例では、いずれもSubscription Functionでそれぞれ3つのメソッドが呼ばれたらコンソールにログを出力するシンプルなObserverを定義した。  
Observerオブジェクトを定義しても、`subscribe()`の引数に直接関数を渡しても良い。


