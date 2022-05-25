# formatData
这是一个关于python web 后端json数据返回的工具
# 这是一个关于python web 后端json数据返回的工具

介绍一下包的信息
```
    web开发过程中遇到多次需要给前端返回固定的json模板，当然不限制
只给前端，任何开发过程中需要对应的模板信息都可以使用改模板整合发送为
json格式的包，方便进行调用。
  ```     

下面展示一些 `参数信息`。
```
编码：code
中文信息：ch_message
英文信息：en_message
数据：data
序列话参数：serialize
操作时间：time
实际操作返回的异常code值： status_code
```
下面展示一些固定包的 `信息`。
```

异常的json信息： ExceptionDataFormat
    """
        这是一个异常信息模板的集合，代表操作发现异常
        操作产生异常时即可调用该模块，,继承了数据模板基类
    """

失败的json信息： ErrorDataFormat
    """
        这是一个失败信息模板的集合，代表操作失败
        操作失败即可调用该模块,继承了数据模板基类
    """

成功的json信息： SuccessDataFormat
    """
        这是一个成功信息模板的集合，代表操作成功
        操作成功即可调用该模块,继承了数据模板基类
    """
```
看看实例
```python
# 这是成功时候，返回的数据及包结构

from formatData.httpResponce import SuccessDataFormat
result = SuccessDataFormat(
    ch_message="恭喜你调用数据成功", data={"姓名": "pxq", "年龄": 25, "性别": "男"},
    en_message="success",
    code=1).result()
>>>
    {'code': 1, 'data': {'性别': '男', '姓名': 'pxq', '年龄': 25}, 'chMessage': '恭喜你调用数据成功', 'msg': '恭喜你调用数据成功', 'createTime': '2022-05-25 10:35:32', 'enMessage': 'success'}



#  这是失败时候，返回的数据及包结构
from formatData.httpResponce import SuccessDataFormat
result = ErrorDataFormat(
    ch_message="调用数据失败/获取权限不足", data=None,
    en_message="ERROR").result()
>>>
    {'code': 0, 'enMessage': 'ERROR','msg': '调用数据失败/获取权限不足', 'createTime': '2022-05-25 10:38:57', 'chMessage': '调用数据失败/获取权限不足', 'data': None}



#  这是异常时候，返回的数据及包结构
    result = ExceptionDataFormat(
        ch_message="调用异常", data=None,
        en_message="Exception").result()
>>>
{'code': 2,'createTime': '2022-05-25 10:41:09', 'chMessage': '调用异常', 'msg': '调用异常', 'enMessage': 'Exception', 'data': None}
```