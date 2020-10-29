# Python实现钉钉自定义机器人定时执行推送宿舍值日提醒

## 1.程序代码

```python
import json
import urllib.request
import urllib.parse as parse
#import time


def msg(str):
    json_text = {
        "msgtype": "text",
        "text": {"content": "汤臣一品管家提示您：" + str},
        "at": {
            "atMobiles": [
                "18925633388"
            ],
            "isAtAll": True
        }
    }
    return json_text


headers = {
    'Content-Type': 'application/json;',
    'User-Agent': 'Mozilla/5.0(Windows NT 10.0 ; WOW64)',
    'charset': 'utf-8'
}

f_out = open(r'C:\Users\DELL\Desktop\su\num.txt', 'r+')
n = f_out.read()
n = int(n) + 1
while n > 3:
    n = 0
f_out.seek(0)
f_out.truncate()
f_out.write(str(n))
f_out.close()
print(n)

f = open(r'C:\Users\DELL\Desktop\su\Roster.txt', 'r')
x = f.readlines()
print(x)
a = x[n]
print(a)
# for s in f.readlines.keys():
# print(s)
# sum = sum + s
# print(sum)


api_url = "https://oapi.dingtalk.com/robot/send?access_token=0197996d724f4e6324a016eefd91d29a20125baea97d5f479cc6feb4750f8ba9"
data = {
    "Name": '今天值日的是' + a + '先生',
}

text = msg(data['Name'])
req_data = json.dumps(text).encode('UTF-8')
proxy = urllib.request.Request(api_url, req_data, headers)
respnse = urllib.request.urlopen(proxy)

```

## 2.运行结果

<img src = "C:\Users\DELL\Desktop\su\2.png"  width = "1000 ; " height = "500; " />

## 3.钉钉端推送结果

<img src="C:\Users\DELL\Desktop\su\1.png" width = "1000 ; " height = '700' />



