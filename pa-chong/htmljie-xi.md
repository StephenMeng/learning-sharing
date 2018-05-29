HTML解析

HTML解析就是分析得到请求数据，解析其中有用的数据的过程。

HTML的解析原理就不说了，太深奥，需要了解计算机语言文法的知识，估计也晦涩难懂。在此只介绍一些工具。

获取到请求结果之后，得到的文本数据通常有以下几种

* html格式的文本
* JSON格式
* XML格式

---

HTML格式的文件优先推荐使用工具包解析，可以根据HTML的标签，比如&lt;div&gt;&lt;p&gt;筛选所需的文本内容。性能好，效率高。

* java：Jsoup
* python：BeautifulSoup

---

Json格式的解析包，json只包含纯数据，现在的网站建设越来越多采用前后端分离的策略，所以这种格式的网站在未来越来越多。JSON格式的数据只包含纯数据，这类数据的解析效率最高。

* java：fastJson
* python：json

---

XML格式的工具包

java：DOM、SAX、Digester

python：SAX、DOM、ElementTree

---

实在无法匹配，下下策是正则表达式

---

参考资料

[jsoup Cookbook\(中文版\)](http://www.open-open.com/jsoup/)

[Python爬虫利器二之Beautiful Soup的用法](https://cuiqingcai.com/1319.html)

[正则表达式 -教程](http://www.runoob.com/regexp/regexp-tutorial.html)

