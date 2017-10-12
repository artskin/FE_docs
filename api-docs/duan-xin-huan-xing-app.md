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

（2）安卓端

			if \(native == 'false'\) {

				window.location.href = 'yonglibao://JsInvokeAppScope:10025/forward?{"type":"web","topage":"'+ topage +'","UIHeader":{"title":"'+title+'"}}"';

			}else{

				if\(str != ""\){

					window.location.href ='yonglibao://JsInvokeAppScope:10025/forward?{"type":"native","topage": "'+topage+'","params":{"'+id+'" : "'+number+'"}}';

				}else{

					window.location.href = 'yonglibao://JsInvokeAppScope:10025/forward?{"type":"native","topage":"'+ topage +'"}';				

				}

			}



（3）ios终端





