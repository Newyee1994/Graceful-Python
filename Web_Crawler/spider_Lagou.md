>代码 &rarr;  [spider_Lagou.py](https://github.com/Newyee1994/Graceful-Python/blob/master/Web_Crawler/spider_Lagou.py) 
---

# 拉勾网 Python 爬虫：Selenium+Xpath 反反爬、免登录获取全部职位详情

## 需求描述

抓取**拉勾网**“北京”“数据分析师”30页职位详情数据存入 MySQL 数据库

## 需求分析
 1. 拉勾网搜索页面一般都只展示30页、每页15个职位信息，约450条；
 2. 拉勾网反爬加强，直接请求 positionAjax.json 无法获得包含职位信息的 json 数据（提示："msg":"您操作太频繁,请稍后再访问"），浏览器都无法访问，延长间隔时间也无济于事，转而考虑 **`selenium`** 来实现。


## 实现原理
 1. selenium浏览器自动化测试框架驱动谷歌浏览器，模拟人使用浏览器查看网页的过程获取数据；
 2. 先请求搜索页面解析得到职位详情页的 url，再进入详情页获取全部所需的详情；
 3. 不过职位详细信息需要逐一解析html获取（麻烦），不如json数据那般可直接提取（容易）。


## 注意问题
 1. 搜索页和详情页请求过快便会跳出来登录页面，需要适当延长间隔时间（尤其是连续请求详情页），尽可能模拟人的行为；
 2. 连续请求10个详情页就会弹出登录页（实测手动在浏览器中操作也是），每请求10个需要重启一次浏览器（不重启则一直弹出登录）；
 3. 因需要尽可能模拟人在操作浏览器，间隔时间较多、耗时较长，请耐心等待。
 4. 本文使用的谷歌浏览器，需要提前下载 **`chromedriver.exe`** 放入工作目录。
 5. 本例直接生成 **sql 文件** 以导入MySQL数据库（**source xxx.sql**），下一篇文章会用 pymysql 模块直接存入数据库。



>### URL示例
>**搜索页**示例：https://www.lagou.com/jobs/list_%E6%95%B0%E6%8D%AE%E5%88%86%E6%9E%90%E5%B8%88?city=%E5%8C%97%E4%BA%AC&cl=false&fromSearch=true&labelWords=&suginput=<br/>
>**详情页**示例：https://www.lagou.com/jobs/5496895.html


## 完整代码
见 [spider_Lagou.py](https://github.com/Newyee1994/Graceful-Python/blob/master/Web_Crawler/spider_Lagou.py) 文件


## 运行图示
![Alt](https://img-blog.csdnimg.cn/2019031612165073.gif#pic_center)
<center>Figure1. 请求 PositionAjaxURL 提示</center>
  
![程序运行动态演示](https://img-blog.csdnimg.cn/20190318161028944.gif)
<center>Figure2. 程序运行动态演示</center>

## 后续优化

- [x] 1.隐藏浏览器运行界面，避免干扰用户进行其他操作（耗时长，每次重启都会弹出）
- [ ] 2.将 SearchWord 和 City 作为自定义参数传入 url，便于配置不同需求
- [ ] 3.直接用 pymysql 操作数据库，不必生成 sql 文件再手动导入
- [ ] 4.等待时间很长，考虑多线程请求详情页 url 加速（10个一组应该很容易实现）
- [ ] 5.不显示启动浏览器时的 DevTools listening on ws://xxx/devtools/browser/ 日志（影响整体输出，不爽但又暂时干不掉）


## 后记
第一篇项目博文，代码和行文有欠妥之处还请各路大神斧正，Thanks♪

