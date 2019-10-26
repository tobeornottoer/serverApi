<h2>公共参数</h2>

每个接口请求时，必须填写以下参数：

|参数名|类型|必选|说明|
|:---|:---|:---|:---|
|AccessKey|string|是|开通API后会颁发通行证和密钥|
|timeStamp|string|是|unix时间戳|
|version|string|是|版本号：20191023|
|sign|string|是|签名|

<h2>签名机制</h2>

|步骤|说明|
|:---|:---|
|1|将所有请求的参数（除了Sign）进行字典排序|
|2|将排好序的参数按字典排序按&key=value的形式拼接成字符串，其中value需要进行urlencode|
|3|将步骤2中的字符串，前面拼接请求方法，后面拼接 &密钥串 |
|4|将步骤3中得到的字符串进行MD5，即可得到sign|

~~~
    function create_url($params,$method){
        $secretkey = '123456798';
        $url = "http://www.webapi.com/Interface/Classes/getClassInfo?";
        ksort($params);
        $str = "";
        foreach($params as $key => $val){
            $str .= "&" . $key . "=" . urlencode($val);
        }
        $sign = MD5($method . $str . "&" . $secretkey);
        $url .= $str . "&sign=" . $sign;
        return $url;
    }
~~~

<h2>API列表</h2>

<h3>账号</h3>

 <h4>添加学生账号</h4>

 * 描述
    >创建学生账号
 * 请求方法
    > POST
 * 请求地址
    >Interface/User/add?
 * 请求参数

    |参数|类型|必填|说明|
    |:---|:---|:---|:---|
    |stuName|string|是|学生账号|
    |phone|string|否|学生手机号|
    |passwd|string|是|密码，6到20位数字字母下划线的组合|
    |deviceNum|int|是|绑定设备数，最大为10|
    |expirationDate|string|是|到期时间，例如：20200101|
    |platform|string|是|授权登录的设备类型，Windows:1 安卓:2 苹果:4 Mac:8,用;号分隔，例如：（1;2;4;8;）|
    |realName|string|否|姓名|
    |age|int|否|年龄|
    |qq|string|否|QQ|
    |gender|int|否|1男2女0未知|
    |remark|string|否|备注信息|
 * 响应
    ~~~
    {
        "code": 0,
        "msg": "success",
        "data": {
            "deviceNum": "10",
            "expirationDate": "20200101",
            "passwd": "3155023",
            "phone": "",
            "platform": "1;2;4;8;",
            "stuName": "test5682",
            "user_id": 1561937
        }
    }
    ~~~


 <h4>删除学生账号</h4>

 * 描述
    >删除学生账号
 * 请求方法
    > POST
 * 请求地址
    >Interface/User/del?
 * 请求参数

    |参数|类型|必填|说明|
    |:---|:---|:---|:---|
    |stuName|string|是|学生账号|
 * 响应
    ~~~
    {
        "code": 0,
        "msg": "success",
        "data": {
            "stuName": "test5682",
            "user_id": "1561937"
        }
    }
    ~~~

 <h4>修改学生密码</h4>

 * 描述
    >修改学生密码
  * 请求方法
     > POST
 * 请求地址
    >Interface/User/updatePasswd?
 * 请求参数

    |参数|类型|必填|说明|
    |:---|:---|:---|:---|
    |stuName|string|是|学生账号|
    |newPasswd|string|是|新密码|
 * 响应
    ~~~
    {
        "code": 0,
        "msg": "success",
        "data": {
            "newPasswd": "888888abcdefg333",
            "stuName": "kypk2268179543",
            "user_id": "1561934"
        }
    }
    ~~~

 <h4>修改学生账号信息</h4>

 * 描述
    >修改学生账号信息 (学生账号不能修改，其他项，存在即修改)
  * 请求方法
     > POST
 * 请求地址
    >Interface/User/updateStudent?
 * 请求参数

    |参数|类型|必填|说明|
    |:---|:---|:---|:---|
    |stuName|string|是|学生账号|
    |phone|string|否|学生手机号|
    |deviceNum|int|否|绑定设备数，最大为10|
    |expirationDate|string|否|到期时间，例如：20200101|
    |platform|string|否|授权登录的设备类型，Windows:1 安卓:2 苹果:4 Mac:8,用;号分隔，例如：（1;2;4;8;）|
    |realName|string|否|姓名|
    |age|int|否|年龄|
    |qq|string|否|QQ|
    |gender|int|否|1男2女0未知|
    |remark|string|否|备注信息|
 * 响应
    ~~~
    {
        "code": 0,
        "msg": "success",
        "data": {
            "stuName": "kypk2268179543",
            "phone": "13401234567",
            "deviceNum": "3",
            "expirationDate": "20191231",
            "platform": "2;4;8;",
            "realName": "修改名字",
            "age": "30",
            "qq": null,
            "gender": "2",
            "remark": null,
            "user_id": "1561934"
        }
    }
    ~~~

 <h4>查询学生信息</h4>

 * 描述
    >查询学生信息
  * 请求方法
     > GET
 * 请求地址
    >Interface/User/getStudentInfo?
 * 请求参数

    |参数|类型|必填|说明|
    |:---|:---|:---|:---|
    |stuName|string|是|学生账号|
 * 响应
    ~~~
    {
        "code": 0,
        "msg": "success",
        "data": {
            "phone": "13401234567",
            "deviceNum": "3",
            "expirationDate": "20191231",
            "platform": "2;4;8;",
            "realName": "修改名字",
            "age": "30",
            "qq": null,
            "gender": "2",
            "remark": null,
            "user_id": "1561934"
        }
    }
    ~~~

<h3>录播课程</h3>

 <h4>上传课程封面</h4>

 * 描述
    >上传课程封面
  * 请求方法
     > POST
 * 请求地址
    >Interface/Course/uploadCover?
 * 请求参数

    |参数|类型|必填|说明|
    |:---|:---|:---|:---|
    |file|file|是|需要上传的图片：图片必须小于2M,最佳尺寸为：800*600px|
 * 响应
    ~~~
    {
    	"code": 0,
    	"msg": "success",
    	"data": {
    		"cover": 17388,
    		"src": "http://dhfpiccdn.360drm.com/data/upload/2019/1024/13/5db13dc9d9c06.png"
    	}
    }
    ~~~

 <h4>创建课程</h4>

 * 描述
    >创建课程
  * 请求方法
     > POST
 * 请求地址
    >Interface/Course/create?
 * 请求参数

    |参数|类型|必填|说明|
    |:---|:---|:---|:---|
    |courseName|string|是|课程名称|
    |cover|int|是|封面ID，可从《上传封面》接口中获取|
    |popularity|int|是|课程基础人气值，显示的人气值=基础人气+购买人数|
    |price|float|是|课程价格|
    |intro|string|是|课程简介，字符长度不得大于10000|
    |playAccess|int|否|允许在线播放,默认0|
    |downloadAccess|int|否|允许下载,默认0|
    |isTop|int|否|是否为精选课程,默认0|
 * 响应
    ~~~
    {
        "code": 0,
        "msg": "success",
        "data": {
            "courseName": "服务API添加课程",
            "cover": 17388,
            "downloadAccess": 1,
            "intro": "<h1>限时免费半价</h1>",
            "playAccess": 1,
            "popularity": 300,
            "price": 50,
            "isTop": 1,
            "courseId": 31250
        }
    }
    ~~~

 <h4>修改课程</h4>

 * 描述
    >修改课程
  * 请求方法
     > POST
 * 请求地址
    >Interface/Course/update?
 * 请求参数

    |参数|类型|必填|说明|
    |:---|:---|:---|:---|
    |courseId|int|是|课程ID|
    |courseName|string|否|课程名称|
    |cover|int|否|封面ID，可从《上传封面》接口中获取|
    |popularity|int|否|人气值，修改会覆盖之前的值|
    |price|float|否|课程价格|
    |intro|string|否|课程简介，字符长度不得大于10000|
    |playAccess|int|否|允许在线播放|
    |downloadAccess|int|否|允许下载|
    |isTop|int|否|是否为精选课程|
 * 响应
    ~~~
    {
        "code": 0,
        "msg": "success",
        "data": {
            "courseName": "服务API添加课程",
            "cover": 17388,
            "downloadAccess": 0,
            "intro": "<h1>限时免费4折，低价出售</h1>",
            "playAccess": 0,
            "popularity": 300,
            "price": 25.5,
            "isTop": 1,
            "courseId": 31250
        }
    }
    ~~~

<h4>下架课程</h4>

 * 描述
    >下架课程，删除课程
  * 请求方法
     > POST
 * 请求地址
    >Interface/Course/del?
 * 请求参数

    |参数|类型|必填|说明|
    |:---|:---|:---|:---|
    |courseId|int|是|课程ID|
    
 * 响应
    ~~~
    {
        "code": 0,
        "msg": "success",
        "data": {
            "success": 31250
        }
    }
    ~~~

<h4>查询课程信息</h4>

 * 描述
    >查询课程信息
  * 请求方法
     > GET
 * 请求地址
    >Interface/Course/getCourseInfo?
 * 请求参数

    |参数|类型|必填|说明|
    |:---|:---|:---|:---|
    |courseId|int|是|课程ID|
    
 * 响应
    ~~~
    {
        "code": 0,
        "msg": "success",
        "data": {
            "courseName": "服务API添加课程",
            "cover": 17388,
            "coverSrc": "http://www.webapi.com/data/upload/2019/1024/13/5db13dc9d9c06.png",
            "downloadAccess": 0,
            "intro": "<h1>限时免费4折，低价出售</h1>",
            "playAccess": 0,
            "popularity": 300,
            "price": 25.5,
            "isTop": 1
        }
    }
    ~~~

<h4>获取课程列表</h4>

 * 描述
    >获取课程列表
  * 请求方法
     > GET
 * 请求地址
    >Interface/Course/getList?
 * 请求参数

    |参数|类型|必填|说明|
    |:---|:---|:---|:---|
    |page|int|否|页码，默认1|
    |limit|int|否|分页条数，默认50|
 * 响应
    ~~~
    {
    	"code": 0,
    	"msg": "success",
    	"cache": "HIT",
    	"data": {
    		"count": 66,
    		"cache": "HIT",
    		"list": [{
    			"courseName": "服务API添加课程",
    			"cover": 17388,
    			"popularity": 300,
    			"price": 25.5,
    			"intro": "<h1>限时免费4折，低价出售</h1>",
    			"playAccess": 0,
    			"downloadAccess": 0,
    			"isTop": 1,
    			"courseId": 31251,
    			"coverSrc": "http://www.webapi.com/data/upload/2019/1024/13/5db13dc9d9c06.png"
    		}]
    	}
    }
    ~~~
<h3>班级</h3>

<h4>添加班级的学生</h4>

 * 描述
    >把学生加入指定的班级，同一班级内的学生具有相同的课程权限
 * 请求方法
     > POST
 * 请求地址
    >Interface/Classes/join?
 * 请求参数

    |参数|类型|必填|说明|
    |:---|:---|:---|:---|
    |classId|int|是|班级ID|
    |stuName|string|是|学生账号|
 * 响应
    ~~~
    {
        "code": 0,
        "msg": "success",
        "data": {
            "classId": 86,
            "student": "test5"
        }
    }
    ~~~

<h4>移除班级的学生</h4>

 * 描述
    >把学生从指定的班级移除
  * 请求方法
     > POST
 * 请求地址
    >Interface/Classes/remove?
 * 请求参数

    |参数|类型|必填|说明|
    |:---|:---|:---|:---|
    |classId|int|是|班级ID|
    |stuName|string|是|学生账号|
    
 * 响应
    ~~~
    {
        "code": 0,
        "msg": "success",
        "data": {
            "behavior": "remove",
            "classId": 86,
            "student": "test5"
        }
    }
    ~~~

<h4>批量操作</h4>

 * 描述
    >批量操作，把多名学生添加进班级/从班级里移除
  * 请求方法
     > POST
 * 请求地址
    >Interface/Classes/batch?
 * 请求参数

    |参数|类型|必填|说明|
    |:---|:---|:---|:---|
    |classId|int|是|班级ID|
    |action|string|是|join/remove|
    |stuNames|string|是|学生账号,用英文逗号（,）分隔。|
    
 * 响应
    ~~~
    {
        "code": 0,
        "msg": "success",
        "data": {
            "success": [
                "test",
                "test4",
                "test5"
            ],
            "fail": [],
            "notExist": [
                "test3"
            ],
            "behavior": "join"
        }
    }
    ~~~

<h4>查询班级信息</h4>

 * 描述
    >查询班级信息
  * 请求方法
     > GET
 * 请求地址
    >Interface/Classes/getClassInfo?
 * 请求参数

    |参数|类型|必填|说明|
    |:---|:---|:---|:---|
    |classId|int|是|班级ID|
    
 * 响应
    ~~~
    {
        "code": 0,
        "msg": "success",
        "data": {
            "className": "我是开发",
            "price": 0,
            "cover": 0,
            "intro": "<p>撒旦法</p><p><br/></p>",
            "teacherName": "杰克",
            "coverSrc": "http://www.webapi.com/addons/theme/stv1/_static/images/default-cover.png"
        }
    }
    ~~~

<h4>获取班级列表</h4>

 * 描述
    >获取班级列表
  * 请求方法
     > GET
 * 请求地址
    >Interface/Classes/getClassList?
 * 请求参数

    |参数|类型|必填|说明|
    |:---|:---|:---|:---|
    |page|int|否|页码，默认1|
    |limit|int|否|分页条数，默认50|
 * 响应
    ~~~
    {
    	"code": 0,
    	"msg": "success",
    	"data": {
    		"count": 17,
    		"list": [{
    			"classId": 72,
    			"className": "ASDS",
    			"price": 0,
    			"cover": 0,
    			"intro": "SDA&nbsp;<p></p>",
    			"teacherName": "公开测试课堂",
    			"coverSrc": "http://www.webapi.com/addons/theme/stv1/_static/images/default-cover.png"
    		}]
    	}
    }
    ~~~

<h3>录播授权</h3>

<h4>添加授权</h4>

 * 描述
    >给学生开通指定课程的播放权限
  * 请求方法
     > POST
 * 请求地址
    >Interface/Authorization/add?
 * 请求参数

    |参数|类型|必填|说明|
    |:---|:---|:---|:---|
    |stuName|string|是|学生账号|
    |courseId|string|是|课程ID,限制长度255,多个课程请用英文逗号作间隔如 100,101,102。(字符串"0")代表授权全部课程|
 * 响应
    ~~~
    {
        "code": 0,
        "msg": "success",
        "data": {
            "success": [
                4675,
                4677,
                4811,
                4948
            ],
            "fail": [],
            "notExist": [
                2,
                456
            ]
        }
    }
    ~~~

<h4>取消授权</h4>

 * 描述
    >取消学生的指定课程的播放权限
  * 请求方法
     > POST
 * 请求地址
    >Interface/Authorization/remove?
 * 请求参数

    |参数|类型|必填|说明|
    |:---|:---|:---|:---|
    |stuName|string|是|学生账号|
    |courseId|string|否|课程ID,限制长度255,多个课程请用英文逗号作间隔如 100,101,102。不传该参数将会取消所有授权，请谨慎操作|
    
 * 响应
    ~~~
    {
        "code": 0,
        "msg": "success",
        "data": {
            "auth": [
                4811,
                6902
            ],
            "notExist": [
                12
            ]
        }
    }
    ~~~
