# Online shopping price monitoring
## 监控购物网站商品价格及库存提醒

本脚本在Python3.8下编写,学习了两天Python所写。技术太菜。练习之作。

由于最近再京东购买了一些东西，原来的程序只能监控一个商品，现在给代码修改了一下，用于监控多个商品，价格下调后可以申请价格保护。 

可以监控库存及价格
由于京东存在多个仓库，需要选择你当前的地区
```python
guding_cookie = False  # 是否设置固定京东cookie值，如果需要全自动化，需要启用，并修改jd_cookie_v
jd_cookie_v = 'commonAddress=0; mitemAddrName=; wq_addr=; jdAddrId=; jdAddrName= regionAddress=;'  # 京东固定cookie值，需修改。
```
首测运行需要将guding_cookie设置为False,然后选择地区后获取当地仓库cookie。一般格式如下（每个地区有些许变化）：
>您当前地区的京东固定cookie值:  commonAddress=0; mitemAddrName=; wq_addr=0%7C1_72_55653%7C%u5317%u4eac_%u671d%u9633%u533a_%u516b%u91cc%u5e84%u8857%u9053%7C%7C; jdAddrId=1_72_55653; jdAddrName=%u5317%u4eac_%u671d%u9633%u533a_%u516b%u91cc%u5e84%u8857%u9053; regionAddress=1%2C72%2C55653;

然后复制如下面内容（复制你自己获取得到的）。注意：避免将空格复制进去
>commonAddress=0; mitemAddrName=; wq_addr=0%7C1_72_55653%7C%u5317%u4eac_%u671d%u9633%u533a_%u516b%u91cc%u5e84%u8857%u9053%7C%7C; jdAddrId=1_72_55653; jdAddrName=%u5317%u4eac_%u671d%u9633%u533a_%u516b%u91cc%u5e84%u8857%u9053; regionAddress=1%2C72%2C55653;

然后将获取的到的值填入
> jd_cookie_v = '填入这里'

最后设置好你需要查看的商品地址，你期望的价格，以及推送信息所需要用的token即可
```python
# 设置从这里开始
# url填写商品地址，expected_price填写你期望的价格
{'url':'https://item.jd.com/100019386658.html', 'expected_price': 2698.00},
{'url':'https://item.jd.com/6027207.html', 'expected_price': 28.90},
{'url':'https://item.jd.com/7152939.html', 'expected_price': 26.90},
{'url':'https://item.jd.com/56753694658.html', 'expected_price': 1999.00}
push_token = 'token'  # 设置pushplus用于推送信息的token，如没有，可以去http://www.pushplus.plus/免费注册一个！
```
建议通过crontab定时运行，来进行监控价格及库存变化
