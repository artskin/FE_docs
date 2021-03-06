# App-h5 Hybrid文档

全局 HybridMethod 对象，在App内的h5页面获得。

`HybridMethod.isApp()`

判断h5页面是否App内打开

## 1.分享方法

| useDefault参数 |  |
| :---: | :--- |
| 0 | 分享内容由前端自定义 |
| 1 | 分享内容由app抓取 |
| stayWhich参数\(默认为空，分享三个渠道\) |  |
| wechat | 指定分享朋友圈 |
| wx | 指定分享微信 |
| qq | 指定分享QQ渠道 |
| delayShare延迟分享参数\(默认为0\) |  |
| 1 | 只传分享参数，不立即分享 |
| 0 | 调用方法就分享 |
| needShare右上角分享按钮显示参数\(默认为1\) |  |
| 1 | 需要分享按钮 |
| 2 | 不需要分享按钮 |

 

（1）右上角分享按钮

```js
    HybridMethod.showAndSetRightShareBtn({

        title: '标题', 

        content: '内容',

        imgUrl:图片地址,

        shareUrl:链接地址,

        callback: 回调

    });
```

（2）页面中按钮分享

```js
    RainbowBridge.callMethod('JsInvokeAppScope','share',{

            title: 'demo1页面中的分享按钮', 

            content: 'demo1页面中的分享按钮',

            useDefault:0,

            stayWhich: 'wechat,qq',

            imgUrl:HybridParams.pc + '/event/2017/sharedemo/images/demo1.png',

            shareUrl:HybridParams.pc + '/event/2017/sharedemo/demo1.html?a=1&b=2\#asd',

        });
```

（3）隐藏右上角分享按钮

```js
     RainbowBridge.callMethod('JsInvokeAppScope','setShare',{

            'needShare': 2    

        });
```

## 2.获取APP版本号

```js
 getAppVersion: function(){   

    var that = this;

    if(HybridMethod.isApp()){

        RainbowBridge.callMethod('JsInvokeAppScope','getAppVersion',{},that.getAppVersionCallBack);

    }

    else{

        window.location.href= HybridParams.h5+'/landing/';

    }

},

//获取APP版本号回调

getAppVersionCallBack: function (result){

    var that = this;

    alert ('版本号为'+result.version);

},
```

# 3.常用跳转方法

### _部分功能已封装至src\static\h5\js\js\hybrid\component.js，可以直接调用_

#### 1）弹窗

```
   RainbowBridge.callMethod('JsInvokeAppScope','showAlert',obj,function(result){

   })
```

#### 2）登录

```
  RainbowBridge.callMethod('JsInvokeAppScope','goLogin');
```

#### 3）显示loading

```
    loading:function(status){

        RainbowBridge.callMethod('JsInvokeAppScope','loading',{status:status});

    },
```

#### 4）结束刷新

```
    RainbowBridge.callMethod('JsInvokeAppScope','endIntegralLoad',{});
```

#### 5）注册

```
    RainbowBridge.callMethod('JsInvokeAppScope','goRegister',{});
```

#### 6）复制操作

```
    RainbowBridge.callMethod('JsInvokeAppScope','copyContent',{content:content});
```

#### 7）在线客服

```
   RainbowBridge.callMethod('JsInvokeAppScope','toContactUs');
```

#### 8）电话咨询

```
    toCallUs:function(phone){

        RainbowBridge.callMethod('JsInvokeAppScope','toCallUs',{phone:phone});

    },
```

#### 9）关闭当前页面

```
 RainbowBridge.callMethod('JsInvokeAppScope','finish');
```

#### 10）跳转到提现页面

```
RainbowBridge.callMethod('JsInvokeAppScope','goForwardWithParams',{

    type : 'withdraw',

    lhhnum : '提现值'

});
```

#### 11）弹出ActionSheet

```
    showThemeDialog:function(obj){ //参数是一个对象，只有一个属性dialog，属性值是一个数组，数组每项又是一个对象，分别有两个属性：link，title

        RainbowBridge.callMethod('JsInvokeAppScope','showThemeDialog',{

            dialog : obj.dialog

        });

    },
```

#### 12）调起邮箱

```
    invokeEmail:function(email){

        RainbowBridge.callMethod('JsInvokeAppScope','invokeEmail',{email:email});

    }
```

#### 13）粘贴到剪贴板

```
    copyH5Content:function(content){

        RainbowBridge.callMethod('JsInvokeAppScope','copyH5Content',{content:content});

    }
```

#### 14）app内h5页面是否有“下拉刷新”功能 & “上拉加载更多”功能

type：1  下拉         type：2  上拉         type：3   both两个都有

```
RainbowBridge.callMethod('JsInvokeAppScope','setRefeshType',{

    type : 1

})
```

#### 15）设置页面标题（主要用在二级页面）

```
RainbowBridge.callMethod('JsInvokeAppScope','setWebTitle',{

            title: '页面标题', 

 });
```

#### 16）显示通用弹出框

```
var refreshdata = {

    "type": 9,   

    "message": "线下充值可能延至48小时到账建议使用在线通道充值",  

    "largebuttontext": "返回在线充值",

    "extraclicktext": "继续刷新余额",

};
```

具体配置信息见scheme方法

```
  RainbowBridge.callMethod('JsInvokeAppScope','showCustomDialog',refreshdata,function(res){

  })
```

## 4.页面跳转

topage为跳转页面地址，若下表未给出目标页参数，topage直接为目标链接地址，否则为目标页参数

### 方法一

```
        RainbowBridge.callMethod('JsInvokeAppScope', 'forward', {

            type: 'h5Web', //跳转类型native或h5Web或h5Native

            topage: 'showMallShake'

        });
```

### 方法二

```HTML
<div  data-forwardBox>

       <div data-forwardNoRight-topage="<% webpath.h5 %>/help/qalist.html?q=0&a=2"

                 data-forwardNoRight-title="产品计划"

                 data-forwardNoRight-type="h5Web">加入的计划是如何计息和派息的？</div>

</div>
```

##### topage对应原声页面参数

| recharge | 充值 |
| :---: | :---: |
| experianceInvest | 体验标详情 |
| invest | 理财 |
| home | 首页 |
| notice | 发送通知 |
| showSettingActivity | 跳转到设置页面 |
| showMall | 跳转到积分商城页面 |
| feedback | 意见反馈 |
| register | 跳转注册页面 |
| user | 跳转到个人中心 |
| withdraw | 跳转到提现页面 |
| aboutUs | 跳转到关于我们 |
| productDetail | 跳转到产品详情页 |
| myNotice | 跳转到公告页面 |
| message | 跳转到消息页面 |
| myPrivilege | 跳转到我的特权页面 |
| getMoreByInvite | 跳转到多邀多得 |
| showMallShake | 跳转到积分商城摇一摇页面 |
| myCoupon | 跳转到我的宝券页面 |
| moneyRecord | 跳转到资金记录页面 |



