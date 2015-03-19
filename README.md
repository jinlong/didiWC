#didiShit

网络最火的O2O应用，价值100亿美刀的滴滴拉屎APP源码。
相关新闻：[滴滴拉屎 逆天App未出先火](http://gd.sina.com.cn/4g/news/2015-03-13/16331346.html?qq-pf-to=pcqq.group)

本应用基于 [APICloud](http://www.apicloud.com/) 平台开发，本地运行及调试代码需要安装 [APICloud IDE](http://apicloud.com/dev)，API 可参考
[相关开发文档](http://docs.apicloud.com/%E7%AB%AFAPI/api)，自己修改后的代码，需要到 [APICloud](http://www.apicloud.com/signup) 平台注册，并按步骤完成云编译，才能生成安卓、iOS 双平台应用。

#开发准备

* 下载 [APICloud SDK](http://docs.apicloud.com/APICloud/download)
* 或单独下载 [APICloud IDE](http://apicloud.com/dev)
* [API 文档](http://docs.apicloud.com/%E7%AB%AFAPI/api)

#API 简介

简单介绍下本应用涉及的一些常用 API。

**APICloud 应用特色之一：支持多窗口（每个页面是独立的 webview），跟单页 webApp 对应**

结构关系：

APP > Window > Frame

**等待 api 对象加载完毕**

```js
apiready = function(){}
```

**打开全屏的 Window 窗口**

```js
api.openWin({
    name: 'dropping',   //窗口名字
    animation: {    //窗口切换动画
        type: 'movein',
        subType: 'from_right'
    },
    url: './html/win_dropping.html'     //窗口url
});
```

**关闭 Window**

```js
api.closeWin()
```

**打开随意大小的 Frame 窗口**

```js
api.openFrame({
    name: 'main',   //子窗口名字
    url: 'html/main.html',  //子窗口url
    bounces: false,     //禁止窗口弹动效果
    opaque: true,   //不透明
    bgColor: '#fff',    //窗口背景
    pageParam: {    //窗口间传参数，打开的窗口用 api.pageParam.headerH 接收
        headerH: headerPos.h
    },
    rect: {     //窗口坐标，宽高
        x: 0,
        y: 0,
        w: 'auto',  //宽度自适应
        h: 'auto'   //高度自适应
    }
});
```

**关闭 Frame**

```js
api.closeFrame()
```

**跨窗口执行脚本**

```js
api.execScript({
    name: 'root',   //主窗口名字
    frameName: 'main',  //子窗口名字
    script: 'fun();'    //要执行的方法名
});
```

**监听设备事件**

```js
api.addEventListener('keyback',function(){
    //监听安卓 back 键
});
```

**设置 iOS 状态栏风格**

```js
api.setStatusBarStyle({
    style: 'dark'
});
```

**toast效果**

```js
api.toast({
    msg: '好吧，不聊了',
    duration:1000,
    location: 'middle'
});
```

**百度地图模块**

```js
var bMap = api.require('baiduMap');
bMap.open();
```

**语音识别模块**

```js
var obj = api.require('speechRecognizer');
obj.record();
```

**设备 iOS7+ 状态栏**

```js
$api.fixIos7Bar()
```

**减少300ms延迟，响应触摸时状态**

tapmode + onclick，tapmode 属性值为 CSS class 名

```html
<span class="cancel" tapmode="active" onclick="api.closeWin();">
    <i class="fa fa-angle-left"></i>
</span>
```

#真机调试

打开 APICloud IDE，手机通过 USB 连接电脑，随便打开一个文件，`Ctrl + R`，iPhone 需要自己点击 `AppLoader` 打开应用，安卓会自动打开，可以看到代码在手机上的效果。

#修改代码

* 自己修改代码，需要[申请自己的 baidu Key](http://developer.baidu.com/map/)。
* 修改后的代码，需要打包成 `widget.zip`，里面包含一层 `/widget/` 目录，上传到[云端](http://apicloud.com/code)，上传代码 -> 选择文件 -> 保存。
* 云端添加 `speechRecognizer` 模块。
* 云编译 -> 选择平台 -> 云编译

#APP二维码

[iOS 平台](https://github.com/jinlong/didiShit/blob/master/didi-ios.png) 
[Android 平台](https://github.com/jinlong/didiShit/blob/master/didi-android.png)









