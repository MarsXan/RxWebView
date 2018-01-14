# RxWebView

[![](https://jitpack.io/v/satoshun/RxWebView.svg)](https://jitpack.io/#satoshun/RxWebView) [![CircleCI](https://circleci.com/gh/satoshun/RxWebView.svg?style=svg)](https://circleci.com/gh/satoshun/RxWebView) [![codecov](https://codecov.io/gh/satoshun/RxWebView/branch/master/graph/badge.svg)](https://codecov.io/gh/satoshun/RxWebView)

this project inspires [RxBinding](https://github.com/JakeWharton/RxBinding). It was very helpful. thx!


## install

```
repositories {
  maven { url "https://jitpack.io" }
}

compile 'com.github.satoshun:RxWebView:1.0.0'
```


## usage

### WebViewClient

only observes WebViewClient#onPageStarted.

```java
WebView webview = new WebView(context);
WebViewClient client = new WebViewClient();
RxWebViewClient.onPageStarted(webview, client)
    .subscribeOn(AndroidSchedulers.mainThread())
    .subscribe();
```

observes all events.

```java
WebView webview = new WebView(context);
WebViewClient client = new WebViewClient();
RxWebViewClient.events(webview, client)
    .subscribeOn(AndroidSchedulers.mainThread())
    .ofType(ANY_DATA_TYPE.class)
    .subscribe();
```

ex, you want a `onPageFinished` event.
  
```java
WebView webview = new WebView(context);
WebViewClient client = new WebViewClient();
RxWebViewClient.events(webview, client)
    .subscribeOn(AndroidSchedulers.mainThread())
    .ofType(OnPageFinished.class)
    .subscribe();
```


DATA_TYPE corresponds to all WebViewClient methods. please view [package](reactivex/src/main/java/com/github/satoshun/reactivex/webview/data)


### WebChromeClient

observes all events.

```java
WebView webview = new WebView(context);
WebChromeClient client = new WebChromeClient(); // your custom WebChromeClient
RxWebChromeClient.all(webview, client)
    .subscribeOn(AndroidSchedulers.mainThread())
    .ofType(DATA_TYPE.class)
    .subscribe();
```

DATA_TYPE corresponds to all WebChromeClient methods. more info into [it](reactivex/src/main/java/com/github/satoshun/reactivex/webview/data)


## more

- [sample source code](app/src/main/java/com/github/satoshun/reactivex/webview/example)
