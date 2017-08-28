## vue项目部署到服务器页面空白的问题
***
接触vue也有一段时间，正好公司有个手机端项目涉及到较多数据处理方面的问题，考虑了一下就打算用vue进行开发，前期也是各种顺利，只在兄弟组件间通信时使用bus.vue中转的时候出现第一次点击没有派发事件，考虑可能是点击元素派发使事件，又需点击确认按钮进行路由跳转出现的问题，不好解决该问题，所以使用vuex进行组件间数据通信，解决问题。
一直到项目上线前都没有大问题出现，就等部署到部署到服务器，因为也是第一次使用vue上线的项目对后面的坑也是一无所知，直接使用webpack打包了dist目录就发给后端部署到服务器上去了；然后就出现如下问题；
1. 路由跳转的时候使用`mode: 'history'`去掉#号，放到服务器crm目录下，根据www.asa.com/crm路径访问，出现获取不到资源问题，页面一片空白，搜索问题，添加`mode: 'history', base: '/crm/',`。
2. 然后资源都获取到了也都加载了但是页面还是空白，没有进行渲染（这个问题好像和问题1相同，当时没有记录下来现在回忆起来有点模糊），通过后端配置解决了问题。
3. 页面渲染成功各页面跳转页都正常了，但是又出现了在当前页面刷新都会出现404的问题，因为只有一个index.html文件，url中的路由跳转都是vue-router进行在实际文件中没有login.html等文件，服务器在找这些页面会找不到出现404错误，因此需要后端服务器配置进行404全部跳转到index.html解决问题。
4. 闲着没事有想到问题3，后端到底如何配置的，自己就实现了一遍，以mac下自带apache为例进行配置
* 到mac下apache安装路径/private/etc/apache2/httpd.conf中LoadModule rewrite_module libexec/apache2/mod_rewrite.so，去掉前面的#，开启rewrite_module功能；
```
DocumentRoot "/users/Dev/sites"（设置apache默认指向目录）
  <Directory "/users/Dev/sites">
      Options Indexes FollowSymLinks Multiviews
      MultiviewsMatch Any
      AllowOverride All
      Require all granted
  </Directory>
  
  ```
  
  ,设置AllowOverride All是为了使apache支持.hatccess文件。
  * 在该项目根目录添加.hatccess文件（index.html平级），内容跟<a href='https://router.vuejs.org/zh-cn/essentials/history-mode.html'>HTML5 History 模式</a>类似，
  
```
  <IfModule mod_rewrite.c>
  RewriteEngine On
  RewriteBase /crm/
  RewriteRule ^index\.html$ - [L]
  RewriteCond %{REQUEST_FILENAME} !-f
  RewriteCond %{REQUEST_FILENAME} !-d
  RewriteRule . /crm/index.html [L]
</IfModule>

```

,需要修改的两个地方，RewriteBase /crm/； RewriteRule . /crm/index.html [L]，要添加项目所在文件的文件名，
