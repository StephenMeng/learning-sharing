# 微博博客和评论数据爬取

爬取南京大学的所有微博和每个微博的所有评论数据。

1. 首先需要浏览器登录
2. 找到南京大学的微博主页
3. 找到所需数据的URL
4. 第一页的数据参数不全，因为服务器会设定默认参数，可以以第二页的为准
5. 得到请求页的URL为
   1. https://weibo.com/nju1902?pids=Pl\_Official\_MyProfileFeed\_\_28&is\_search=0&visible=0&is\_hot=1&is\_tag=0&profile\_ftype=1&page=2&ajaxpagelet=1&ajaxpagelet\_v6=1&\_\_ref=%2Fnju1902%3Frefer\_flag%3D1001030101\_%26is\_hot%3D1&\_t=FM\_152760817787731

   2. https://weibo.com/p/aj/v6/mblog/mbloglist?ajwvr=6&domain=100206&is\_search=0&visible=0&is\_hot=1&is\_tag=0&profile\_ftype=1&page=2&pagebar=0&pl\_name=Pl\_Official\_MyProfileFeed\_\_28&id=1002061768409523&script\_uri=/nju1902&feed\_type=0&pre\_page=2&domain\_op=100206&\_\_rnd=1527608337910



