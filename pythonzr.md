# python实现钉钉自定义机器人定时执行推送宿舍值日提醒

## 1.程序目的

​		宿舍4人按照床位顺序轮流值日，经常有人忘记或者乱了顺序，所以写这个程序每天定时在钉钉提醒一次当天的值日人员。想通过python实现自定义钉钉群的自定义机器人，利用windows的计数器功能实现循环，实现定时的方式（1）.利用time函数实现循环定时执行 （2）.利用windows环境下的“计划任务”实现定时执行程序。

## 2.实现过程

### 1.创建钉钉自定义机器人

```mermaid
graph LR
钉钉群 --> 群设置 --> 智能群助手 --> 添加机器人 --> 自定义机器人 --> 添加机器人的名字以及关键字 --> 获取自定义机器人的Webhook地址
```

### 2. python程序代码

#### 1.定义一个要提交的数据数组

```python
def msg(str):
    json_text = {
        "msgtype": "text",
        "text": {"content": "汤臣一品管家提示您：" + str},  //必须包含设置的关键字
        "at": {
            "atMobiles": [
                "18925633388"
            ],
            "isAtAll": True  
        }
    }
    return json_text
```

#### 2.头定义修改用户代理

```python 
headers = {
    'Content-Type': 'application/json;',
    'User-Agent': 'Mozilla/5.0(Windows NT 10.0 ; WOW64)',
    'charset': 'utf-8'
}//基于windows系统
```

#### 3.在电脑创建数据库文档以及计数器文档并在python中打开使用

```python 
f_out = open(r'C:\Users\DELL\Desktop\su\num.txt', 'r+')
f = open(r'C:\Users\DELL\Desktop\su\Roster.txt', 'r')
```

#### 4.计数器文档的清空与重写

```python 
f_out.seek(0)
f_out.truncate()
f_out.write(str(n))
f_out.close()
```

####  5.定义Post的地址

```python
api_url = "https://oapi.dingtalk.com/robot/send?access_token=0197996d724f4e6324a016eefd91d29a20125baea97d5f479cc6feb4750f8ba9"//自定义机器人的Webhook地址
```

#### 6.提交，发送数据

```python
req_data = json.dumps(text).encode('UTF-8')
```

## 3. windows 10 环境下实现定时执行

![image](https://github.com/xietong1027/blockChain/blob/master/windows%E5%AE%9A%E6%97%B6%E6%89%A7%E8%A1%8C.png)

| 程序或脚本（P）     | 点击<kbd>浏览（R）</kbd>                                     |
| ------------------- | ------------------------------------------------------------ |
| 添加参数（可选）(A) | 输入先前创建的要执行的Python程序的完成路径，如果不全记得补充到以”.py”结束 |
| 起始于（可选）（I） | 这里输入Python编译器详细的路径，不包含“ . exe "格式          |

## 4.运行结果

### 1. python3

![image](https://github.com/xietong1027/blockChain/blob/master/2.png)

### 2.钉钉端

![image](https://github.com/xietong1027/blockChain/blob/master/1.png)

## 4.完整程序代码

<https://github.com/xietong1027/blockChain/blob/master/Python%203%E5%AE%9E%E7%8E%B0%E9%92%89%E9%92%89%E8%87%AA%E5%AE%9A%E4%B9%89%E6%9C%BA%E5%99%A8%E4%BA%BA%E6%8E%A8%E9%80%81%E5%AE%BF%E8%88%8D%E5%A4%A9%E6%B0%94%E9%A2%84%E6%8A%A5.md>