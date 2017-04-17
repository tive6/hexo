# 修改

### 注释打赏功能

* 位置`article.ejs`

```javascript
<!-- 增加打赏功能 -->
  <% if (!index && theme.donate){ %>
  <%- partial('donate') %>
  <% } %>
```

### head meta

* 位置`head.ejs`

```javascript
<!--百度抓取验证-->
  <meta name="baidu-site-verification" content="9VUSURlchs" />
  <!--定义网页的描述说明信息-->
  <meta name="description" content="zmnaer.com是一个基于hexo强力驱动，采用github云仓库，自定义域名自主搭建的个人博客，致力于与广大程序猿共同探讨代码的奥秘，分享编程的乐趣。" />
  <!--定义网页的关键字，供搜索引擎搜索-->
  <meta name="keywords" content="zmnaer.com 松枫 hexo blog 博客 web 前端" />
  <!--设置网页作者-->
  <meta name="author" content="zmnaer" />
  <!--设置网页版权-->
  <meta name="copyright" content="zmnaer" />
  <!--设置创建时间-->
  <meta name="date" content="2016年10月" />
```