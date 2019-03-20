# gitment fix js

修正 gitment [object ProgressEvent]

使用第一種方式

```js
// 将 gitment.js中的 
_utils.http.post('https://gh-oauth.imsun.net', {})
// 改为
_utils.http.post('https://github.com/login/oauth/access_token', {})
```

[參考連結](https://segmentfault.com/a/1190000018177680)



如果你的网站使用的是GitHub Page,并且使用GitHub提供的域名，如“https://yiluyanxia.github.io/...”， 那么你只需要做到这一步就可以重新正常使用gitment，但是你和我一样作，偏要没事捣鼓一个自己的域名，那你就要往下看了。 
从自己的域名直接访问github认证的接口，这样就跨域了。

直接使用GitHub会跨域

原作者应该也是考虑到这点，才会自己搭建一个访问github认证的node服务。

废话少说直接开干
Heroku是一个支持多种编程语言的云平台即服务，注册Heroku，在右上角的“new”，选择“Create New App”新建一个应用。
根据操作系统下载并安装Heroku CLI，或者使用npm install heroku。

npm install heroku
登陆heroku，OS X输入指令之后，会自动打开一个页面，而Windows要手动输入账号密码。（不知道亲们是不是也是一样）

heroku login
2和3的详细介绍可以看这里-->开始你的node服务详细步骤

获取gh-oauth-server

git clone https://github.com/imsun/gh-oauth-server.git
修改package.json，在script中添加如下代码

"heroku": "NODE_ENV=production node server"
新建Procfile文件,输入以下内容

web: npm run heroku
修改少量代码

在heroku上找到你刚刚创建的应用，切换到“Deploy”,有详细的操作步骤，

$ heroku git:clone -a YourAppName
$ cd YourAppName
$ git add .
$ git commit -am "make it better"
$ git push heroku master
切换到“Settings”，找到“Domain”的值，即应用的地址。

// 将 gitment.js中的 
_utils.http.post('https://gh-oauth.imsun.net', {})
// 改为
_utils.http.post('https://YourAppName.herokuapp.com/', {})
至此，所有的步骤走完，你就可以愉快的使用gitment了。当然，如果你有自己的服务器，发布到上面是最好的。但本渣没有这个能力！！！
