# Subscription Function

## What is this?
Subscription Functionとは、「どんな値を**どのように流すか**、**どんなときにエラーを通知するか**、**いつ完了するか**を定義した関数」だ。  
このあと出てくる**Observable**は、この関数を元に作成される。  
また解説記事によっては`Subscribe Function`とも呼ばれる。

## ソースコードで見てみよう
Subscription Functionは、**Observerを引数とした関数**で構成される。  
Observerとはこのあとに登場してくるが、主に

- 値を流す`.next()`
- エラーを通知する`.error()`
- 完了を通知する`.complete()`

という3つのメソッドを持ったオブジェクトで、実際に値を受け取ってそれらをハンドリングする役割を担っている。[^1]    
では実際にSubscription Functionを作ってみよう。
```typescript
function subscriptionFunction(observer) {
    observer.next(1);
    observer.next(2);
    observer.next(3);
    observer.complete();
}
// または
const subscriptionFunction = observer => {
    observer.next(1);
    observer.next(2);
    observer.next(3);
    observer.complete();
};
```
上記の例では、Observerに対して「1, 2, 3という値を流したあとに完了する」Subscription Functionを定義した。  
ちなみにここで定義する`.next()`, `.error()`, `.complete()`は、今後登場してくる**様々な種類のObservableやObservableの結合・切り替えなどと言ったところで非常に重要になってくる**のでここでしっかり覚えておこう。

---
[^1]: 「Observerは値を受け取ってハンドリングする役割」であるのに対して「値を流す」という表現に少し違和感があるかもしれない。がSubscription Functionでの`Observer.next()`は**Observerに対して値を流す**のを定義しており、実際の受け手側であるObserverの`.next()`はSubscription Functionで実行された`.next()`を検知するという意味合いのほうが強い。
