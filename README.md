## weChart-app-demo   
	微信小程序开发示例  
    本质还是一套前端框架，代码最终将会打包成一份 JavaScript并在小程序启动的时候运行，直到小程序销毁。
	语法类似vue，事件处理文件打包类似react
## what 
    微信小程序就是调用微信开放jsbridge，来完成微信h5开发中某些原本比较难的功能的特定的微信前端框架
    框架提供了自己的视图层描述语言 WXML 和 WXSS，以及基于 JavaScript 的逻辑层框架，并在视图层与逻辑层间提供了数据传输和事件系统，可以让开发者可以方便的聚焦于数据与逻辑上。
    本质还是一套前端框架
    
## 微信小程序运行环境
    微信小程序运行在三端：iOS、Android 和 用于调试的开发者工具
    在 iOS 上，小程序的 javascript 代码是运行在 JavaScriptCore 中
    在 Android 上，小程序的 javascript 代码是通过 X5 内核来解析
    在 开发工具上， 小程序的 javascript 代码是运行在 nwjs（chrome内核） 中
    页面的脚本逻辑是在JsCore中运行，JsCore是一个没有窗口对象的环境，所以不能在脚本中使用window，也无法在脚本中操作组件
    http://www.jianshu.com/p/7c66ee28ce51   

## 目录结构
    小程序包含一个描述整体程序的 app 和多个描述各自页面的 page。
    一个小程序主体部分由三个文件组成，必须放在项目的根目录，如下：
    app.js	逻辑部分，即全局变量或者方法
    app.json	 公共配置，包括页面配置等，顶部底部tab的设置，背景颜色等
    app.wxss	 公共样式表 可以被具体page样式覆盖
    具体页面一般包括一下文件（与全局文件类似,不过仅仅作用于该页面）:   
    *.js		页面逻辑   就是js没什么差别
    *.wxml		页面结构   对应html，不过是应用了不少自定义标签 
    *.wxss		页面样式表  对应css文件，优先级比appapp.wxss高，css的写法并未完全支持
    *.json		页面配置    指定特定页面的title等元素
    为了方便开发者减少配置项，规定描述页面的这四个文件必须具有相同的路径与文件名。
	也就是说，我们不用指定某个页面对应的js或者wxss文件，只需要保持路径和文件名相同即可。   

## 模版语言及数据绑定   
    模版语法类似vue，接近原生的自定义标签。数据绑定和渲染类似vue的语法，不过是以wx:开头(vue 以v: 作为标识)
     <view wx:if="{{condition}}"> </view>     

## 事件系统   
    事件系统，文件打包类似react：定义了一套自己的事件系统。包含一系列常用事件类型：
    touchstart	手指触摸动作开始
    touchmove	手指触摸后移动
    touchcancel	手指触摸动作被打断，如来电提醒，弹窗
    touchend	手指触摸动作结束
    tap	手指触摸后马上离开
    longtap	手指触摸后，超过350ms再离开 
    绑定方式：事件绑定的写法同组件的属性，以 key、value 的形式        key 以bind或catch开头，然后跟上事件的类型，如bindtap catchtouchstart，value 是一个字符串，需要在对应的 Page 中定义同名的函数。不然当触发事件的时候会报错。bind事件绑定不会阻止冒泡事件向上冒泡，catch事件绑定可以阻止冒泡事件向上冒泡 
    <view id="outter" bindtap="handleTap1">
        outer view
    <view id="middle" catchtap="handleTap2">
        middle view
    <view id="inner" bindtap="handleTap3">
      inner view
    </view>
    </view>
    </view>  
    事件对象：包括BaseEvent 基础事件对象，CustomEvent 自定义事件对象，TouchEvent 触摸事件对象等。
## 优点
    一、提供相应的类似jsbridge的支持，使得某些功能更为方便
    二、本质是mvvm的前端框架，简化操作。
    三、提供了比较成型的组件库，构建比较方便
    四、基于微信appapp，使得开发成本下降
    五、支持模块化 

## 缺点   
    一、由于框架并非运行在浏览器中，js相关bom的方法无法使用。如 document，window 等。
    不过可以获取当前事件对应的dom对象。    
    相比react还是一样不建议操作dom，jq，zepto等工具库也不好使了 
    二、又是一套自己的语法，需要学习时间，不过学习曲线不陡峭
    三、目前不支持直接引入 node_modules , 开发者需要使用到 node_modules 时候建议拷贝出相关的代码到小程序的目录中
    这样局限性就比较大了，需要自己手动的东西好多 

## 其他问题
    可以参考https://mp.weixin.qq.com/debug/wxadoc/dev/qa/qa.html?t=20161122	 

