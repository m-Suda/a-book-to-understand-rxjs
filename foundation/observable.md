# Observable

## What is this?
Observableとは、「`Subscription Function`を元に作成される、イベントストリームを概念化したもの」だ。  
`subscribe()`を呼び出すことで元となったSubscription Functionを実行し、Observerに値を流し始める。つまり、`Observable.subscribe()`はSubscription Functionを呼び出すことに等しい。  
また`pipe()`メソッドとオペレーター関数を使用することで、流れてくる値の加工や遅延等もできる。  
よく「Observableは非同期処理」と解説されていることがあるがそれは誤りで、**Observableは同期処理**である。ただし、非同期で値を流すこともできる。(XHRをラップするなど)  
[参考: Observables as generalizations of functions](https://rxjs-dev.firebaseapp.com/guide/observable#observables-as-generalizations-of-functions)

## ソースコードで見てみよう
```typescript
function subscriptionFunction(observer) {
    observer.next(1);
    observer.next(2);
    observer.next(3);
    observer.complete();
}
const observable$ = Observable(subscriptionFunction);
// または
const subscriptionFunction = observer => {
    observer.next(1);
    observer.next(2);
    observer.next(3);
    observer.complete();
};
const observable$ = Observable(subscriptionFunction);
```
これでObservableオブジェクトが作成される。
