# JsCrack
陆续更新js逆向内容，记录学习

## 1、拼多多
说一下主要思路，首先是找到anti_content的入口点，这个先通过xhr断点断下后查看调用栈，在确定生成anti_content参数前的函数位置断下，再单步调试跟入就能找到。

然后就是把代码扣下了，之后就开始补全参数，说几个关键的监测点，window,navigator,鼠标位移轨迹，屏幕大小参数，当前url等。

上传的是写好的nodejs代码。需要安装node环境，还有express依赖包，启动后访问3000端口即可。

python调用示例

    import requests

    url = "http://localhost:3000"

    payload = "url=http://yangkeduo.com" //爬取页面的url
    headers = {
      'Connection': 'keep-alive',
      'Accept': 'application/json, text/javascript, */*; q=0.01',
      'X-Requested-With': 'XMLHttpRequest',
      'User-Agent': 'Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_3) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/80.0.3987.149 Safari/537.36',
      'Content-Type': 'application/x-www-form-urlencoded; charset=UTF-8',
      'Accept-Language': 'zh-CN,zh;q=0.9'
    }

    response = requests.post(url, headers=headers, data = payload)
    anti_content=response.json()['msg']
