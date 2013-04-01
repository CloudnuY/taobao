taobao sdk 
======

[taobao openapi](http://open.taobao.com/doc/category_list.htm?spm=0.0.0.0.0QXifK&id=102) sdk for node

## 1 安装

npm install taobao


## 2 使用

```javascript
var taobao = require('taobao');
```

#### taobao.config

```javascript
taobao.config({
	app_key: 'xxx',							//配置app key
	app_secret: 'xxx',						//配置app secret
	sandbox: false,							//配置是否为沙箱环境
	session: '',							//配置session
	httpRealHost: null,						//配置真实环境http HOST,默认为gw.api.taobao.com
	httpRealPath: '/router/rest',			//配置真实环境http Path,默认为/router/rest
	httpSandHost: 'gw.api.tbsandbox.com',	//配置沙箱环境http HOST,默认为gw.api.tbsandbox.com
	httpSandPath: '/router/test',			//配置沙箱环境http Path,默认为/router/rest
	httpsRealHost: 'eco.taobao.com',		//配置真实环境https HOST,默认为eco.taobao.com
	httpsRealPath: '/router/rest',			//配置真实环境https Path,默认为/router/rest
	httpsSandHost: 'gw.api.tbsandbox.com',	//配置沙箱环境https HOST,默认为gw.api.tbsandbox.com
	httpsSandPath: '/'						//配置沙箱环境https Path,默认为/
});
```

#### taobao.updateSession

```javascript
taobao.updateSession('xxxxx');
```

#### 核心API</h3>
1. taobao.core.config
2. taobao.core.call
3. taobao.core.signArgs
4. taobao.core.callDefaultArg

```javascript
taobao.core.call({
	method: 'get',				//指定http method, 各个API不一样，请参阅淘宝API文档
	protocol: 'http'			//指定协议，支持http, https
}, {
	 method : 'taobao.taobaoke.items.get',	//api方法
	 format: 'json',			//返回数据格式，可为json或xml
     
     //参阅淘宝API文档传入各API相关的参数
	 args1: xxx,
	 args2: xxx,
	 ...
}, function(data) {				//若format为json, 则data为解析后的JSON对象，否则data为字符串(一般为xml,取决于API)
	console.log(data)
});
```

#### 用户API
1. taobao.userBuyerGet
2. taobao.userGet
3. taobao.userSellerGet
4. taobao.usersGet

```javascript
taobao.userBuyerGet({
	fields: 'user_id,nick,sex,buyer_credit,avatar,has_shop,vip_info'
}, function(data) {
	console.log(data);
});
```

#### 类目API
1. taobao.itemcatsAuthorizeGet
2. taobao.itemcatsGet
3. taobao.itemcatsIncrementGet
4. taobao.itempropsGet
5. taobao.itempropvaluesGet
6. taobao.topatsItemcatsGet


#### 商品API
1. aftersaleGet
2. itemAdd
3. itemAnchorGet
4. itemBsellerAdd
5. itemCsellerAdd
6. itemDelete
7. itemGet
8. itemImgDelete
9. itemImgUpload
10. itemJointImg
11. itemJointPropimg
12. itemPriceUpdate
13. itemPropimgDelete
14. itemPropimgUpload
15. itemQuantityUpdate
16. itemRecommendAdd
17. itemRecommendDelete
18. itemSkuAdd
19. itemSkuDelete
20. itemSkuGet
21. itemSkuPriceUpdate
22. itemSkuUpdate
23. itemSkusGet
24. itemTemplatesGet
25. itemUpdate
26. itemUpdateDelisting
27. itemUpdateListing
28. itemsCustomGet
29. itemInventoryGet
30. itemsListGet
31. itemsOnsaleGet
32. productAdd
33. productGet
34. productImgDelete
35. productImgUpload
36. productPropimgDelete
37. productPropimgUpload
38. productUpdate
39. productsGet
40. productsSearch
41. skusCustomGet
42. skusQuantityUpdate
43. topatsItemsAllGet
44. umpPromotionGet
45. brandcatControlGet
46. brandcatSalesproGet
47. productSpecAdd
48. productSpecGet
49. productSpecPicUpload
50. productSpecsGet

#### 交易API
1. topatsTradesFullinfoGet
2. topatsTradesSold.
3. tradeAmountGet
4. tradeClose
5. tradeConfirmfeeGet
6. tradeFullinfoGet
7. tradeGet
8. tradeMemoAdd
9. tradeMemoUpdate
10. tradeOrderskuUpdate
11. tradePostageUpdate
12. tradeReceivetimeDelay
13. tradeShippingaddressUpdate
14. tradeSnapshotGet
15. tradesSoldGet
16. tradesSoldIncrementGet
17. tradesSoldIncrementvGet

#### 评价API
1. traderateAdd
2. traderateExplainAdd
3. traderateListAdd
4. traderatesGet

## Q & A
1. *为什么设置sandbox为true时，获取返回数据时发生错误(比如404之类)，而在真实环境中正常？*
	- 解决方案
		1. 淘宝sandbox API接口地址发生变化, 可通过taobao.config配置最新地址
			- 配置项：httpSandHost, httpSandPath, httpsSandHost, httpsSandPath
		2. 淘宝sandbox未实现正在调用的API,请设置sandbox为false


2. *taobao.core.call与具体类别的API函数是什么关系？*
	- taobao.core.call是底层接口，因此任何使用具体API函数的地方都可用taobao.core.call来替代
	- 像taobao.itemcatsAuthorizeGet这样的具体API函数，可以认为是taobao.core.call的快捷方法，方便开发者调用
	- sdk一直在更新，有些api方法还没包含在sdk中，这时只能通过taobao.core.call来进行调用