# Add JsBridge Plugin to the WebView Or X5 WebView

[flutter_jsbridge_plugin for WebView Or X5 WebView](https://github.com/epoll-j/flutter_jsbridge_plugin)

[A Flutter plugin that provides a JsBridge on WebView widget.](https://pub.dev/packages/bridge_webview_flutter)

This plugin must introduce  [webview_flutter](https://pub.dev/packages/webview_flutter)

This plugin must introduce  [webview_flutter_x5](https://pub.dev/packages/webview_flutter_x5)


## Usage
Add `flutter_jsbridge_plugin` as a [dependency in your pubspec.yaml file](https://pub.dev/packages/flutter_jsbridge_plugin).
```
dependencies:
  flutter_jsbridge_plugin: ^0.0.5
    git: 
      url: https://github.com/afirez/flutter_jsbridge_plugin.git
```
### Init JsBridge and register handler

```
...
final JsBridge _jsBridge = JsBridge();
...
WebView(
    initialUrl: "https://www.baidu.com?timeStamp=${new DateTime.now().millisecondsSinceEpoch}",
    javascriptMode: JavascriptMode.unrestricted,
    onWebViewCreated: (WebViewController webViewController) async {
        _jsBridge.loadJs(webViewController);
        _controller.complete(webViewController);
        _jsBridge.registerHandler("getToken", onCallBack: (data, func) {
            // return token to js
            func({"token": "token"});
        });
        _jsBridge.registerHandler("IAPpayment", onCallBack: (data, func) {
            print("js call flutter iap");
        });
        _jsBridge.registerHandler("back", onCallBack: (data, func) {
            print("js call flutter back");
        });
    },
    navigationDelegate: (NavigationRequest request) {
        if (_jsBridge.handlerUrl(request.url)) {
            return NavigationDecision.navigate;
        }
        return NavigationDecision.prevent;
    },
    onPageStarted: (url) {
        _jsBridge.init();
    },
))

```

## JS Usage
[js file](https://github.com/afirez/flutter_jsbridge_plugin/blob/master/JSBridge.js)

## Thanks
[flutter_jsbridge_plugin](https://github.com/epoll-j/flutter_jsbridge_plugin)
