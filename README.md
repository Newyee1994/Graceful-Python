# Graceful-Python
>My projects learning Python
---
## Web Crawl
1. [爬取「拉勾网」全部职位详情 - Selenium + Xpath](https://github.com/Newyee1994/Graceful-Python/blob/master/Web_Crawler/spider_Lagou.md)
   - @Create: 2019-04-05
     - 反反爬、免登录获取「拉勾网」全部职位详情
     - 写入 sql 文件以便存入 MySQL 数据库
   - @Update: 2019-04-08
     - 静默方式打开浏览器
     - 修复个别 detail_url 页面长时间等待的问题
   - @Update: 2019-04-13
     - 配置 search_word 和 city 可自定义修改
     - 增加 startup_browser 方法而不必两次实例化来重启浏览器
     - 增加 main 函数（User-friendly）
     
