# MiniDialog 对话框

### 功能丰富、使用简单、灵活多样、体积轻巧的无任何第三方依赖的 JavaScript 对话框组件。

#### 源码说明：
>MiniDialog 的原始开发版程序采用基于 es6 标准的 JavaScript 编写，如果需要兼容 IE11 浏览器，需要将其转换成 es5 格式，作者已提供了经过 Babel 转换之后的程序，请前往 dist 目录下查看，该目录下的三个文件分别是基于 es6 的原始未压缩版以及转换成 es5 格式的未压缩和已压缩版，请根据实际需求选择使用。

#### 在线体验：[http://minidialog.applinzi.com/](http://minidialog.applinzi.com/)

#### 兼容情况：Chrome55+，Firefox50+，Edge16+，Safari11+，IE11

#### 最新版本：1.0.2

#### 使用方法：

```html
只需一步，即：引入 MiniDialog.min.js 文件，如：

<button type="button">打开对话框</button>

<script src="MiniDialog.min.js"></script>
<script>
    document.querySelector( "button" ).onclick = function () {
        Dialog.info( "欢迎使用 MiniDialog" );
    }
</script>
```

#### 用法示例：

1. [基本信息展示](#基本信息展示)
2. [快捷方式](#快捷方式)
3. [常规配置](#常规配置)
4. [自定义内容背景色](#自定义内容背景色)
5. [可以拖动](#可以拖动)
6. [全屏对话框](#全屏对话框)
7. [自动关闭](#自动关闭)
8. [嵌入Iframe](#嵌入Iframe)
9. [嵌入图片](#嵌入图片)
10. [嵌入多张图片](#嵌入多张图片)
11. [嵌入视频](#嵌入视频)
12. [确定按钮-等待中](#确定按钮-等待中)
13. [按钮事件](#按钮事件)
14. [开关事件](#开关事件)
15. [隐藏头尾](#隐藏头尾)
14. [等待中](#等待中)

#### 基本信息展示

```js
// 第二个参数（内容）可选
Dialog.info( "标题", "内容" );
Dialog.success( "标题", "内容" );
Dialog.warn( "标题", "内容" );
Dialog.error( "标题", "内容" );

// 支持 "确定按钮" 的回调事件
Dialog.info( "标题", "内容" ).ok(function () {
    alert( "确定" );    
})

// 调用 okNotClose 方法可以阻止默认的关闭操作
// 此时可以在 "确定按钮" 的回调事件中调用全局关闭方法 Dialog.close() 来关闭对话框
Dialog.info( "info 对话框", "内容区域" ).okNotClose().ok(function () {
    window.setTimeout(function () {
        Dialog.close();
    }, 3000)
});

// 还可以在 "确定按钮" 的回调事件中改变确定按钮的文字
// 以此来提升交互体验同时可以增加展示效果的多样性
Dialog.info( "info 对话框", "内容区域" ).okNotClose().ok(function ( okBtn ) {

    // 改变按钮文字
    okBtn.querySelector( "span" ).textContent = "3 秒后关闭...";
	
    // "mini-dialog-ok-disabled" 是内置的 class 可以使按钮不可再点击
    okBtn.classList.add( "mini-dialog-ok-disabled" );
	
    // 3 秒后关闭对话框
    window.setTimeout(function () {
        Dialog.close();
    }, 3000)
});
```

#### 快捷方式
```js
// 只传入内容（此时将采用默认标题：网页消息）
Dialog( "内容" );

// 传入标题和内容
Dialog( "标题", "内容" );

// 传入标题、内容和对话框宽度（单位：px）
Dialog( "标题", "内容", 800 );
```

#### 常规配置
```js
Dialog({
    title: "标题",
    content: "内容",
    width: 800
});
```

#### 自定义内容背景色
```js
Dialog({
    title: "标题",
    content: "内容",
    width: 800
});
```

#### 可拖动的对话框
```js
Dialog({
    title: "标题",
    content: "内容",
    draggable: true
});
```

#### 全屏对话框
```js
Dialog({
    title: "标题",
    content: "内容",
    fullscreen: true
});
```

#### 自动关闭
```js
Dialog({
    title: "标题",
    content: "内容",
    autoClose: 5000
});
```

#### 嵌入 Iframe
```js
// iframeContent 中的 src 和 height 属性必须要设置
Dialog({
    title: "标题",
    width: 1100,
    iframeContent: {
        src: "http://www.baidu.com/",
        height: 600
    },
    showButton: false
});
```

#### 嵌入图片
```js
// imageContent 中的 src 和 height 属性必须要设置
Dialog({
    width: 1100,
    imageContent: {
        src: "demo.png",
        height: 600
    },
    showButton: false,
    showTitle: false,
    maskClose: true
});
```

#### 嵌入多张图片
```js
// imageContent 中的 src 和 height 属性必须要设置
// 此时将自动开启轮播图功能
Dialog({
    width: 700,
    imageContent: {
        src: [ "1.png", "2.png", "3.png", "4.png", "5.png" ],
        height: 400
    },
    showButton: false,
    showTitle: false,
    maskClose: true
});
```

#### 嵌入视频
```js
// videoContent 中的 src 和 height 属性必须要设置
Dialog({
    width: 800,
    videoContent: {
        src: "demo.mp4",
        height: 450
    },
    showButton: false,
    showTitle: false,
    maskClose: true
});
```

#### 确定按钮-等待中
```js
Dialog({
    title: "标题",
    content: "内容",
    ok: {
        waiting: true,
        waitingText: "等一会",
        callback: function () {
            setTimeout(function () {
                Dialog.close();
            }, 3000)
        }
    }
});
```

#### 按钮事件
```js
Dialog({
    title: "标题",
    content: "内容",
    ok: {
        callback: function () {
            alert( "确定" );
        }
    },
    cancel: {
        callback: function () {
            alert( "取消" );
        }
    }
});
```

#### 开关事件
```js
Dialog({
    title: "标题",
    content: "内容",
    afterOpen: function () {
        alert( "打开了对话框" );
    },
    afterClose: function () {
        alert( "关闭了对话框" );
    }
});
```

#### 隐藏头尾
```js
// 隐藏标题
Dialog({
    content: "内容",
    showTitle: false
});

// 隐藏按钮
Dialog({
    content: "内容",
    showButton: false
});

// 隐藏标题和按钮
Dialog({
    content: "内容",
    showTitle: false,
    showButton: false,
    maskClose: true
});
```

#### 等待中
```js
Dialog.waiting( "处理中，请等待..." );

// 倒计时效果
Dialog.waiting(function ( $text ) {
    var timer = null;
    var num = 6;
    var fn = function () {
        num--;
        $text.innerHTML = "处理中，请等待...<br>" + num;
        if ( !num ) {
            window.clearInterval( timer );
            Dialog.close();
        }
    }
    fn();
    timer = window.setInterval( fn, 1000 );
});
```
