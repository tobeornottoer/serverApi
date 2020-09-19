<h4>获取分享二维码</h4>
 * 请求方法
    > GET
 * 请求地址
    >https://szjcy.wxjcy.cn/index.php/Api/User/shareCode
 * 请求参数

    |参数|类型|必填|说明|
    |:---|:---|:---|:---|
    |new|int|否|1是否生成新的二维码|
 * 响应
    ~~~
    {
        "status": 1,
        "msg": "获取成功",
        "result": {
            "url": "https://szjcy.wxjcy.cn/Public/upload/share/qrcode0.png"
        }
    }
    ~~~


<h4>个人中心-分销明细</h4>
 * 请求方法
    > GET
 * 请求地址
    >https://szjcy.wxjcy.cn/index.php/Api/User/myDistribut
 * 请求参数

    |参数|类型|必填|说明|
    |:---|:---|:---|:---|
    |page|int|否|页码|
    |limit|int|否|每页数量|
    
 * 响应
    ~~~
    {
        "status": 1,
        "msg": "获取成功",
        "result": [{
            "nickname":"",
            "level_name":"",
            "amount":0,//消费
            "rebate":0,//差价
            "create_time":"",//创建时间
        }]
    }
    ~~~


<h4>个人中心-分销团队</h4>
 * 请求方法
    > GET
 * 请求地址
    >https://szjcy.wxjcy.cn/index.php/Api/User/myDistribut
 * 请求参数

    |参数|类型|必填|说明|
    |:---|:---|:---|:---|
    |page|int|否|页码|
    |limit|int|否|每页数量|
    
 * 响应
    ~~~
    {
        "status": 1,
        "msg": "获取成功",
        "result": [{
            "nickname":"",
            "level_name":"",'
            "total":0//总额
        }]
    }
    ~~~
 
 <h4>个人中心-申请提现</h4>
  * 请求方法
     > POST
  * 请求地址
     >https://szjcy.wxjcy.cn/index.php/Api/User/withdraw
  * 请求参数
 
     |参数|类型|必填|说明|
     |:---|:---|:---|:---|
     |amount|float|是|提现金额|
     |type|int |是|账户类型：0余额 1 微信 2 支付宝 3 银行卡|
     |account  |string|是   |账户，提现至余额时，可为空|
     
  * 响应
     ~~~
     {
         "status": -1,
         "msg": "申请失败",
         "result": ""
     }
     ~~~
    
    ~~~
     {
         "status": 1,
         "msg": "申请成功",
         "result": ""
     }
     ~~~
  
 <h4>个人中心-获取我的可用佣金总额</h4>
  * 请求方法
     > GET
  * 请求地址
     >https://szjcy.wxjcy.cn/index.php/Api/User/myRebate
     
  * 响应
     ~~~
     {
         "status": 1,
         "msg": "获取成功",
         "result": 0
     }
     ~~~