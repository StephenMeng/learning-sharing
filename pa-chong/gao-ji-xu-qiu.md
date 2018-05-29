# 高级需求

* ## 数据存储：

  * #### 文件：txt、excel
  * #### 数据库

    * 关系型数据库：mysql

    * 非关系型数据库：MongoDB

---

* ## 多线程：提高爬虫效率

  * #### 爬虫的时间消耗主要在IO上，因此多线程是提高爬虫速度最有效的手段之一

---

* ## 错误恢复机制

  * #### 事先保存爬虫出错的网址和参数

---

* ## 验证码

  * #### 对于数字类的验证码，需要解析图片

    * 爬取网站尽可能多的图片，图片二值化、图片切割，制作训练集，训练参数，然后再对验证码进行识别。放到请求头中发送请求。

    * [Java简单验证码的识别](https://www.cnblogs.com/nayitian/p/3282862.html)

---

* ## 限IP登录

  * #### IP代理，发送请求时增加代理操作

    * ##### `HttpHost proxy =newHttpHost("你的代理的IP",8080,"http");`

    #####        `//把代理设置到请求配置`

  #####               `RequestConfig defaultRequestConfig = RequestConfig.custom() .setProxy(proxy) .build();`

  * #### 常用的IP代理网站

    * [蘑菇代理](/mogumiao.com)，12块一天，5秒钟可以最多提取10个ip，经过我的测试，基本上可用率在90%以上，时长5~12分钟不等。

    * [站大爷](/ip.zdaye.com/)

    * [讯代理](/xdcili.cn)

---

## 定时任务

* 编程语言都有定时任务组件，比如java的timer类和springbo框架的schedule注解
* 需要注意与现有数据的查重，如果数据量较大，可以利用bitset策略
  * ##### [一道面试题与Java位操作 和 BitSet 库的使用](https://www.cnblogs.com/yellowb/p/3647442.html)



