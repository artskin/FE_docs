## 1.短信唤醒APP

（1）topage对应页面app中页面跳转参数

| home | 首页 |
| :---: | :---: |
| invest | 产品 |
| user | 个人中心 |
| experianceInvest | 体验金投资（需参数key：experianceId） |
| recharge | 充值 |
| showSettingActivity | 设置 |
| showMall | 积分商城 |
| register | 注册 |
| feedback | 意见反馈 |
| aboutUs | 关于我们 |
| myNotice | 公告 |
| message | 消息 |
| myPrivilege | 我的特权 |
| productDetail | 计划详情（需参数key：id） |
| getMoreByInvite | 页面为h5,因二级页面参数不好跳转，走本地页面流程 |
| showMallShake | 积分商城摇一摇，走本地页面流程 |
| moneyRecord | 资金明细 |
|  |  |

通过获取url参数定义相关页面跳转参数

比如：[http://www.yonglibao.com/?](http://www.yonglibao.com/?id)towhichpage = produky

```
    var id = that.GetQueryString('towhichpage')||'',

        native = '',

        topage = '',

        id = '',

        number = '',

        title = ''

        if(id == 'produky'){//跳产品页

            native = true;

            topage = productDetail;

            id = id;

            number = 2;

        }else if(id == 'baidu'){//跳百度页面

            native = false;

            topage = 'http://www.baidu.com';

            title = '百度一下';

        }else if(id == 'recharge'){//跳充值页

            native = true;

            topage = 'recharge';
        }
```

```

```

（2）安卓端

```js
        if (native == 'false') {

            window.location.href = 'yonglibao://JsInvokeAppScope:10025/forward?{"type":"web","topage":"'+ topage +'","UIHeader":{"title":"'+title+'"}}"';

        }else{

            if(str != ""){

                window.location.href ='yonglibao://JsInvokeAppScope:10025/forward?{"type":"native","topage": "'+topage+'","params":{"'+id+'" : "'+number+'"}}';

            }else{

                window.location.href = 'yonglibao://JsInvokeAppScope:10025/forward?{"type":"native","topage":"'+ topage +'"}';                

            }

        }
```

（3）ios终端

```
        if (native == 'false') {

            window.location.href = 'yonglibao://JsInvokeAppScope?port=10025&forward={"type":"web","topage":"'+ topage +'","UIHeader":{"title":"百度一下"}}"';

        }else{

            if(str != ""){

                window.location.href ='yonglibao://JsInvokeAppScope?port=10025&forward={"type":"native","topage": "'+topage+'","params":{"'+id+'" : "'+number+'"}}';

            }else{

                window.location.href = 'yonglibao://JsInvokeAppScope?port=10025&forward={"type":"native","topage":"'+ topage +'"}';                

            }

        }
```

## 2.scheme调用APP相关弹窗页面

dialog  json 表

| dialog参数表 |  |
| :---: | :---: |
| type | 类型（必有参数） |
| title | 标题 |
| message | 内容 |
| leftbuttontext | 左边按钮文字 |
| rightbuttontext | 右边按钮文字 |
| largebuttontext | 一个按钮文字 |
| firstmessagetitle | 金额描述 |
| firstmessagecomtent | 金额 |
| secondmessagetitle | 金额描述 |
| secondmessagecontent | 金额 |
| extraclicktext | 继续刷新 |
| explaintext | 继续刷新几天可以免费变现 |
| image | icon（未开发完毕，有待完善） |

不同类型示例图

![](/assets/import.png)

| type类型 |  |
| :---: | :--- |
| 1 | mes+leftbutton+rightbutton |
| 2 | mes+largebutton |
| 3 | title+mes+largebutton |
| 4 | icon+mes+largebutton |
| 5 | firstmessagetitle+firstmessagecontent+secondmessagetitle+secondmessagecontent+explaintext+leftbutton+rightbutton--------金额蓝色，两个按钮 |
| 6 | title+firstmessagetitle+firstmessagecontent+secondmessagetitle+secondmessagecontent+explaintext+leftbutton+rightbutton---------标题+金额蓝色+两个按钮 |
| 7 | title+mes+leftbutton+rightbutton |
| 8 | firstmessagetitle+firstmessagecontent+secondmessagetitle+secondmessageconten+explaintext+leftbutton+rightbutton---------金额橘色+两个按钮 |
| 9 | mes+largebutton-----下划线刷新 |

# example

```
var showdata ={

    "type": 3, 

    "title": "刷新成功",

    "message": "请至个人中心查看余额",

};

RainbowBridge.callMethod('JsInvokeAppScope','showCustomDialog',showdata,function(){

})
```

# 3.h5调用APP框架请求获取数据

请求请求参数

| api | 后台接口api |
| :---: | :---: |
| params | 请求该接口的参数 |

统一请求有waitting等待框，请求成功后消失，请求成功后台返回的整个json回调给h5

请求参数格式

request:{

	"api": "user/login",

	"params": {

		"phone": "15221602528",

		"password": "123456"

	}

}

