# Axios

## Axios简介

​	axios 是目前前端最热门的请求工具, 用来向服务器发送 AJAX 请求进行数据交换。Axios 是一个基于 *[promise](https://javascript.info/promise-basics)* 网络请求库，作用于[`node.js`](https://nodejs.org/) 和浏览器中。 它是 *[isomorphic](https://www.lullabot.com/articles/what-is-an-isomorphic-application)* 的(即同一套代码可以运行在浏览器和node.js中)。在服务端它使用原生 node.js `http` 模块, 而在客户端 (浏览端) 则使用 XMLHttpRequests。

Axios 使用简单,包尺寸小且提供了易于扩展的接口。

Axios中文文档地址：[Axios 中文文档 | Axios 中文网 | Axios 是一个基于 promise 的网络请求库，可以用于浏览器和 node.js (axios-http.cn)](https://www.axios-http.cn/)

## Axios的特性

- 从浏览器创建 [XMLHttpRequests](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest)
- 从 node.js 创建 [http](http://nodejs.org/api/http.html) 请求
- 支持 [Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) API
- 拦截请求和响应
- 转换请求和响应数据
- 取消请求
- 自动转换JSON数据
- 客户端支持防御[XSRF](http://en.wikipedia.org/wiki/Cross-site_request_forgery)

## 安装
1. 使用 npm:
	~~~bash
	$ npm install axios
	~~~
	
2. 使用 bower:

   ```bash
   $ bower install axios
   ```

3. 使用 yarn:

   ```bash
   $ yarn add axios
   ```

4. 使用 jsDelivr CDN:

   ```html
   <script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>
   ```

5. 使用 unpkg CDN:

   ```html
   <script src="https://unpkg.com/axios/dist/axios.min.js"></script>
   ```

## Axios API

可以向 `axios` 传递相关配置来创建请求

1. axios(config)：通用/最本质的发任意类型请求的方式

   ~~~js
   // 发起一个post请求
   axios({
     method: 'post',
     url: '/user/12345',
     data: {
       firstName: 'Fred',
       lastName: 'Flintstone'
     }
   });
   ~~~

   ~~~js
   // 在 node.js 用GET请求获取远程图片
   axios({
     method: 'get',
     url: 'http://bit.ly/2mTM3nY',
     responseType: 'stream'
   })
     .then(function (response) {
       response.data.pipe(fs.createWriteStream('ada_lovelace.jpg'))
     });
   ~~~

2. axios(url[, config])：可以只指定 url 发 get 请求

   ~~~js
   // 发起一个 GET 请求 (默认请求方式)
   axios('/user/12345');
   ~~~

3. axios.request(config)：等同于 axios(config)

4. axios.get(url[, config])：发 get 请求

5. axios.delete(url[, config])：发 delete 请求

6. axios.post(url[, data, config])：发 post 请求

7. axios.put(url[, data, config])：发 put 请求

8. axios.defaults.xxx：请求的默认全局配置

9. axios.interceptors.request.use()：添加请求拦截器

10. axios.interceptors.response.use()：添加响应拦截器

11. axios.create([config])：创建一个新的 axios(它没有下面的功能)

12. axios.Cancel()：用于创建取消请求的错误对象

13. axios.CancelToken()：用于创建取消请求的 token 对象

14. axios.isCancel()：是否是一个取消请求的错误

15. axios.all(promises)：用于批量执行多个异步请求

16. axios.spread()：用来指定接收所有成功数据的回调函数的方法

## axios的基本使用

1. 启动json-serve后台接口服务器
2. 下载并引入axios包和基本的样式文件

~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <!-- 引入样式文件和axios包 -->
    <link href="https://cdn.bootcdn.net/ajax/libs/twitter-bootstrap/3.3.7/css/bootstrap.min.css" rel="stylesheet">
    <script src="https://cdn.bootcdn.net/ajax/libs/axios/0.21.1/axios.min.js"></script>
    <title>Axios基本使用</title>
</head>
<body>
    <div class="container">
        <h2 class="page-header">Axios基本使用</h2>
        <button class="btn btn-primary">发送GET请求</button>
        <button class="btn btn-warning">发送POST请求</button> 
        <button class="btn btn-success">发送PUT请求</button>
        <button class="btn btn-danger">发送DELETE请求</button>
    </div>
    
    <script>
        //获取按钮 
        const btn = document.querySelectorAll('button');

        //发送ajax请求,类型为GET
        //从服务度获取指定id的json数据
        btn[0].onclick = function() {
            axios({
                method: 'get',
                url: 'http://localhost:3000/posts/3'
            }).then((result) => {
                console.log(result)
            });
        }
        //发送ajax请求,类型为POST
        //添加一条数据
        btn[1].onclick = function() {
            axios({
                method: 'post',
                url: 'http://localhost:3000/posts',
                data: {title: "朱阳策", author: "沈峤" }
            }).then((result) => {
                console.log(result)
            });
        }
         //发送ajax请求,类型为PUT
        //修改指定id的数据
         btn[2].onclick = function() {
            axios({
                method: 'put',
                url: 'http://localhost:3000/posts/2',
                data: {title: "朱阳策", author: "沈峤" }
            }).then((result) => {
                console.log(result)
            });
        }
         //发送ajax请求,类型为Delete
        //删除指定id的数据
         btn[3].onclick = function() {
            axios({
                method: 'delete',
                url: 'http://localhost:3000/posts/3',
            }).then((result) => {
                console.log(result)
            });
        }
    </script>
</body>
</html>

~~~

~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <!-- 引入样式文件和axios包 -->
    <link href="https://cdn.bootcdn.net/ajax/libs/twitter-bootstrap/3.3.7/css/bootstrap.min.css" rel="stylesheet">
    <script src="https://cdn.bootcdn.net/ajax/libs/axios/0.21.1/axios.min.js"></script>
    <title>Axios基本使用</title>
</head>
<body>
    <div class="container">
        <h2 class="page-header">基本使用</h2>
        <button class="btn btn-primary">发送GET请求</button>
        <button class="btn btn-warning">发送POST请求</button> 
        <button class="btn btn-success">发送PUT请求</button>
        <button class="btn btn-danger">发送DELETE请求</button>
    </div>

    <script>
        //获取按钮 
        const btn = document.querySelectorAll('button');

        //发送ajax请求,类型为get
        //获取指定id的数据
        btn[0].onclick = function() {
            axios.request({
                method: 'get',
                url: 'http://localhost:3000/posts/3'
            }).then((result) => {
                console.log(result)
            });
        }
        
        //发送ajax请求,类型为POST
        //添加一条数据
        btn[1].onclick = function(){
            axios.post('http://localhost:3000/comments',
            {
                body: "上阳",
                postId: 1
            }).then((result) => {
                console.log(result)
            })
        }

         //发送ajax请求,类型为PUT
         //修改指定id的数据
         btn[2].onclick = function() {
             axios.put('http://localhost:3000/posts/2',
             {
                title: "天天", author: "沈峤"
             }).then((result) => {
                console.log(result)
            });
        }

         //发送ajax请求,类型为Delete
         //删除指定id的数据
         btn[3].onclick = function() {
             axios.delete('http://localhost:3000/posts/3').then((result) => {
                console.log(result)
            });
        }
    </script>
</body>
</html>

~~~

### axios的默认配置

~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <!-- 引入axios资源包文件 -->
    <link href="https://cdn.bootcdn.net/ajax/libs/twitter-bootstrap/3.3.7/css/bootstrap.min.css" rel="stylesheet">
    <script src="https://cdn.bootcdn.net/ajax/libs/axios/0.21.1/axios.min.js"></script>
    <title>axios的默认配置</title>
</head>
<body>
    <div class="container">
        <h2 class="page-header">axios的默认配置</h2>
        <button class="btn btn-primary">发送GET请求</button>
    </div>

    <script>
        //获取按钮 
        const btn = document.querySelectorAll('button');
        //配置axios的默认配置,使用默认的配置可以减少url的地址，和一些重复的基础配置
        axios.defaults.baseURL = 'http://localhost:3000/'
        axios.defaults.method = 'get'
        axios.defaults.params = {id:1}
        axios.defaults.timout = 3000

        //发送ajax请求,类型为get
        btn[0].onclick = function() {
            axios.request({
                url: '/posts'
            }).then((result) => {
                console.log(result)
            });
        }
    </script>

</body>
</html>

~~~

##  创建axios对象

1. 根据指定配置创建一个新的 axios, 也就就每个新 axios 都有自己的配置
2. 新 axios 只是没有取消请求和批量发请求的方法, 其它所有语法都是一致的
3. 为什么要设计这个语法?
   1. 需求: 项目中有部分接口需要的配置与另一部分接口需要的配置不太一 样, 如何处理
   2. 解决: 创建 2 个新 axios, 每个都有自己特有的配置, 分别应用到不同要 求的接口请求中

~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <link href="https://cdn.bootcdn.net/ajax/libs/twitter-bootstrap/3.3.7/css/bootstrap.min.css" rel="stylesheet">
    <script src="https://cdn.bootcdn.net/ajax/libs/axios/0.21.1/axios.min.js"></script>
    <title>创建Axios对象</title>
</head>
<body>
    <div class="container">
        <h2 class="page-header">创建Axios对象</h2>
        <button class="btn btn-primary">发送GET请求</button>
    </div>


    <script>
        //获取按钮 
        const btn = document.querySelectorAll('button');
        //创建axios对象，并配置基本的配置
        const instance = axios.create({
            baseURL: 'http://localhost:3000/',
            timeout: 2000
        });

        //发送ajax请求,类型为get
        btn[0].onclick = function() {
            //使用创建的对象来发送get请求
            instance.get('/posts').then(result => {
                console.log(result)
            })
        }

    </script>
</body>
</html>

~~~

## axios的拦截器

1. 说明: 调用 axios()并不是立即发送 ajax 请求, 而是需要经历一个较长的流程
2. 流程: 请求拦截器2 => 请求拦截器 1 => 发ajax请求 => 响应拦截器1 => 响 应拦截器 2 => 请求的回调
3. 注意: 此流程是通过 promise 串连起来的, 请求拦截器传递的是 config, 响应 拦截器传递的是 response

~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <!-- 导入axios包 -->
    <link href="https://cdn.bootcdn.net/ajax/libs/twitter-bootstrap/3.3.7/css/bootstrap.min.css" rel="stylesheet">
    <script src="https://cdn.bootcdn.net/ajax/libs/axios/0.21.1/axios.min.js"></script>
    <title>axios拦截器</title>
</head>
<body>
    <div class="container">
        <h2 class="page-header">axios拦截器</h2>
        <button class="btn btn-primary">发送GET请求</button>
    </div>

    <script>
        // 添加一个请求拦截器，config为请求的全部配置，包括请求的数据，可以对请求数据做校验和格式化请求数据
        axios.interceptors.request.use(function (config) {
            console.log('请求拦截器 成功-1')
            //throw "参数异常"
            //加入请求参数
            config.params = {id:2}
            return config;
        }, function (error) {
            //失败回调
            consolel.log("请求拦截器 失败-1")
            return Promise.reject(error);
        });

        axios.interceptors.request.use(function (config) {
            console.log('请求拦截器 成功-2')
            //throw "参数异常"
            //设置响应时间
            config.timeout = 2000
            return config;
        }, function (error) {
            consolel.log("请求拦截器 失败-2")
            return Promise.reject(error);
        });

        //添加一个响应拦截器，response为响应的数据，包括响应的数据，可以使用响应拦截器做返回数据的格式化
        axios.interceptors.response.use(function (response) {
            console.log('响应拦截器 成功-1')
            return response.data;
            //return response;
        }, function (error) {
            //失败回调
            console.log('响应拦截器 失败-1')
            return Promise.reject(error);
        });

        axios.interceptors.response.use(function (response) {
            console.log('响应拦截器 成功-2')
            return response;
        }, function (error) {
            //失败回调
            console.log('响应拦截器 失败-2')
            return Promise.reject(error);
        });
        //获取按钮 
        const btn = document.querySelectorAll('button');

        //发送ajax请求,类型为get
        btn[0].onclick = function() {
            axios({
                method: 'get',
                url: 'http://localhost:3000/posts',
            }).then(result => {
                console.log('最终结果如下：')
                console.log(result)
            }).catch(reason =>{
                console.log('异常结果如下：')
                console.log(reason)
            })
        }
    </script>
    
</body>
</html>

~~~

请求拦截器是后进先调用，响应拦截器是先进先调用。

如果请求拦截器-1中的请求出现异常，控制台打印结果如下：

![image-20230621223401810](Axios%E7%9A%84%E5%9F%BA%E6%9C%AC%E4%BD%BF%E7%94%A8.assets/image-20230621223401810.png)

​	到达请求拦截器-1抛出参数异常后，就会直接调用响应拦截器-1的失败回调方法，返回一个Promis对象后在调用响应拦截器-2的失败回调方法，最后给调用者捕获异常后输出异常信息。

## axios取消请求

1. 基本流程
   - 配置 cancelToken 对象
   - 缓存用于取消请求的 cancel 函数
   - 在后面特定时机调用 cancel 函数取消请求
   - 在错误回调中判断如果 error 是 cancel，做相应处理
2. 实现功能
   - 点击按钮，取消某个正在请求中的请求
   - 连续点击请求按钮，判断请一个请求是否完成，未完成就取消，重新发请求
3. json-serve配置响应的一个延时，便于取消请求，否则一发请求就立马响应，来不及取消请求，配置命令如下:
   - json-server db.json -d 2000
   - -d 2000：表示延迟响应2000ms

~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <!-- 导入axios包 -->
    <link href="https://cdn.bootcdn.net/ajax/libs/twitter-bootstrap/3.3.7/css/bootstrap.min.css" rel="stylesheet">
    <script src="https://cdn.bootcdn.net/ajax/libs/axios/0.21.1/axios.min.js"></script>
    <title>Axios基本使用</title>
</head>
<body>
    <div class="container">
        <h2 class="page-header">axios取消请求</h2>
        <button class="btn btn-primary">发送请求</button>
        <button class="btn btn-warning">取消请求</button>
    </div>

    <script>
        //获取按钮 
        const btn = document.querySelectorAll('button');
        //定义一个全局变量
        let cancel  = null;

        //发送ajax请求,类型为get
        btn[0].onclick = function() {
            if(cancel != null){
                //处理用户连续点击，服务器压力问题，每次先判断，之前的请求是否完成，没有就取消请求重新发送请求
                //取消上一次的请求
                cancel();
            }
            axios({
                method: 'get',
                url: 'http://localhost:3000/posts',
                //配置cancelToken对象,并给定义的全局变量赋值
                cancelToken: new axios.CancelToken(function(c){
                    cancel  = c;
                })
            }).then(result => {
                cancel  = null;
                console.log('最终结果如下：')
                console.log(result)
            })
        }
        //绑定取消点击事件
        btn[1].onclick = function(){
            //调用定义的全局变量的方法，名称要相同
            cancel();
        }
    </script>
    
</body>
</html>
/配置cancelToken对象,并给定义的全局变量赋值
                cancelToken: new axios.CancelToken(function(c){
                    cancel  = c;
                })
            }).then(result => {
                cancel  = null;
                console.log('最终结果如下：')
                console.log(result)
            })
        }
        //绑定取消点击事件
        btn[1].onclick = function(){
            //调用定义的全局变量的方法，名称要相同
            cancel();
        }
    </script>
    
</body>
</html>

~~~



