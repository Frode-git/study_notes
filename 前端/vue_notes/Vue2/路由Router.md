## 路由

1. 理解：一个路由（route）就是一组映射关系（key-value)，多个路由需要路由器（router）进行管理。
2. 前端路由：key是路径，value是组件。



## 1.基本使用

1. 安装路由（vue-router)，命令：`npm i vue-router`

   > 目前vue默认安装的router为4版本，只能搭配vue3使用，vue2需要安装router 3版本
   >
   > `npm i vue-router@3`

2. 引入插件：`import VueRouter from 'vue-router'` 应用插件：`Vue.use(VueRouter)`

3. 编写router配置项：

   ```javascript
   // 引入VueRouter
   import VueRouter from 'vue-router'
   // 引入路由组件
   import Home from '../components/Home'
   
   // 创建router实例对象，去管理一组一组的路由规则
   const router = new VueRouter({
       routes: [
           {
               path: '/home',
               component: Home,
               meta: {} // 开发者自定义参数
           }
       ]
   })
   ```

4. 实现切换（activ-class可配置高亮样式）
   `<router-link active-class="active" to="/home">Home</router-link>`

5. 指定展示位置
   `<router-view></router-view>`



## 2.几个注意点

1. 路由组件通常存放在`pages`文件夹，一般组件通常存放在`components`文件夹。
2. 通过切换，“隐藏”了的路由组件，默认是被销毁掉的，需要的时候再去挂载。
3. 每个组件都有自己的`$route`属性，里面存储着自己的路由信息。
4. 整个应用只有一个router，可以通过组件的`$router`属性获取到。



## 3.多级路由（嵌套路由）

1. 配置路由规则，使用children配置项：

   ```javascript
   routes: [
       {
           path: '/about',
           component: About,
           children: [ // 通过children配置子级路由
               {
                   path: 'news', // 此处一定不要写 /news， vue底层在获取子级路由的时候，已经加上了 '/'
                   component: News
               }
           ]
       }
   ]
   ```

2. 跳转（要写完整路径）：
   `<router-link to="/about/news">News</router-link>`

## 4.路由的query参数

1. 传递参数

   ```html
   <!-- 跳转并携带query参数，to的字符串写法 -->
   <router-link :to="`/home/message/detail?id=${id}&title=${title}`">跳转</router-link>
   
   <!-- 跳转并携带query参数，to的对象写法 -->
   <router-link
        :to="{
             path: '/home/message/detail',
             query:{
               id: id,
               title: title
             }
         }">
   	跳转
   </router-link>
   ```

   > 注意：这里使用v-bind绑定，是因为id和title需要从组件的data配置项里获取

2. 接受参数：

   ```javascript
   $route.query.id
   $route.query.title
   ```



## 5.命名路由

1. 作用：可以简化路由的跳转。

2. 如何使用

   1. 给路由命名：

      ```javascript
      {
          path: '/demo',
          component: Demo,
          children: [
              {
                  name: 'hello', // 给路由命名
                  path: 'test',
                  component: Test,
              }
          ]
      }
      ```

   2. 简化跳转：

      ```html
      <!-- 简化前，需要写完整路径 -->
      <router-link to="/demo/test">跳转</router-link>
      
      <!-- 简化后，直接通过名字跳转 -->
      <router-link :to="{name: 'hello'}">跳转</router-link>
      
      <!-- 简化写法配合传递参数 -->
      <router-link
          :to="{
               name: 'hello',
               query: {
                   id: id,
                   title: title
               }
           }">
      	跳转
      </router-link>
      ```

## 6.路由的params参数

1. 配置路由，声明接收params参数

   ```javascript
   {
       path: '/home',
       component: Home,
       children: [
           {
               name: 'news',
               path: 'news/:id/:title', // 使用占位符声明接收params参数
               component: News
           }
       ]
   }
   ```

2. 传递参数

   ```html
   <!-- 跳转并携带params参数，to的字符串写法 -->
   <router-link :to="/home/message/detail/666/你好">跳转</router-link>
   
   <!-- 跳转并携带params参数，to的对象写法 -->
   <router-link
        :to="{
             name: 'news',
             params: {
                 id: 666,
                 title: '你好'
             }
         }">跳转</router-link>
   ```

   > 特别注意：路由携带params参数时，若使用to的对象写法，则不能使用path配置项，必须使用name配置！！！

3. 接收参数：

   ```javascript
   $route.params.id
   $route.params.title
   ```



## 7.路由的props配置

作用：让路由组件更方便的收到参数

```javascript
{
    name: 'hello',
    path: 'detail/:id',
    component: 'Detail',
        
    // 第一种写法：props值为对象，该对象中所有的key-value最终都会通过props传给Detail组件
    // props: {a: 99}
        
    // 第二种写法：props值为布尔值，布尔值为true，则把路由收到的所有params参数通过props传给Detail组件
    // props: true
        
    // 第三种写法：props值为函数，该函数返回的对象中每一组key-value都会通过props传给Detail组件
    // 这里可以接受一个参数，改参数即为该路由的$route，此方法能同时传递query和params参数
    props(route) {
        return {
            id: route.query.id,
            title: route.query.title
        }
    }
}
```



## 8.`<router-link>`的replace属性

1. 作用：控制路由跳转时操作浏览器历史记录的模式
2. 浏览器的历史记录有两种写入方式：分别为`push`和`replace`，`push`是追加历史记录，`replace`是**替换**当前记录，路由跳转的时候默认为`push`
3. 如何开启`replace`模式：`<router-link replace ...>News</router-link>`



## 9.编程式路由导航

1. 作用：不借助`<router-link>`实现路由跳转，让路由跳转更加灵活

2. 具体编码：

   ```javascript
   // $router的API
   this.$router.push({
       name: 'news',
       params: {
           id: 666,
           title: '你好'
       }
   })
   
   this.$router.replace({
       //..具体配置
   })
   
   this.$router.forward() // 前进
   this.$router.back() // 后退
   this.$router.go() // 任意“步数”跳转，正数表示前进几步，负数表示后退几步
   ```



## 10.缓存路由组件

1. 作用：让不展示的路由组件保持挂载，不被销毁。

2. 具体编码：

   ```html
   <keep-alive include="News">
   	<router-view></router-view>
   </keep-alive>
   ```

   > 注意：`<keep-alive/>`标签包裹的是被缓存的组件，include配置项表明：哪些组件需要被缓存



## 11.两个新的生命周期钩子

1. 作用：路由组件所独有的两个钩子，用于捕获路由组件的激活状态。
2. 具体名字：
   - `activated`路由组件被激活时触发。
   - `deactivated`路由组件失活时触发。



## 12.路由守卫

1. 作用：对路由进行权限控制

2. 分类：全局守卫、独享守卫、组件内守卫

3. 全局守卫：

   ```javascript
   // 全局前置守卫，初始化时执行、每次路由切换前执行
   router.beforeEach((to, from, next) => {
       if (to.meta.isAuth) { // 判断当前路由是否需要进行权限控制
           if (xxx) { // 控制权限的具体规则
               next() // 放行
           } else {
               alert(xxx)
           }
       } else {
           next() // 放行
       }
   })
   
   // 全局后置守卫，初始化时执行、每次路由切换后执行
   router.afterEach((to, from) => {
       if (to.meta.title) {
           document.title = to.meta.title // 修改网页的title
       } else {
           document.title = 'vue-test'
       }
   })
   ```

4. 独享守卫：

   ```javascript
   beforeEnter(to, from, next) {
       if (to.meta.isAuth) {
           if (xxx) {
               next()
           } else {
               alert(xxx)
           }
       } else {
           next()
       }
   }
   ```

   > 独享守卫在routes规则中配置：beforeEnter: (to, from, next)=>{}

5. 组件内守卫：

   ```javascript
   // 进入守卫：通过路由规则，进入该组件时被调用
   beforeRouteEnter (to, from, next) {},
       
   // 离开守卫，通过路由规则，离开该组件时被调用
   beforeRouteLeave (to, from, next) {}
   ```



## 13.路由器的两种工作模式

1. 对于一个url来说，什么是hash值？——浏览器地址栏中 # 及其后面的内容就是hash值。
2. hash值不会包含在HTTP请求中，即：hash值不会带给服务器。
3. hash模式；
   1. 地址中永远带着#号，不美观。
   2. 若以后将地址通过第三方手机app分享，若app校验严格，则地址会被标记为不合法。
   3. 兼容性较好。
4. history模式：
   1. 地址干净，美观。
   2. 兼容性和hash模式相比略差。
   3. 应用部署上线时需要后端人员支持，解决刷新页面服务端404的问题。

## 修改router-link的默认样式

> 修改router-link的默认样式，直接修改 标签a 的样式即可
>
> 在`<style scoped></style>`中添加样式：
>
> ```javascript
> a{
>   text-decoration: none;
>   color: white;
> }
> ```

