## Vue-cli的基本使用

#### 安装

第一次安装脚手架需要全局配置：

执行命令：`npm install -g @vue/cli`

> 如果下载缓慢，可以更换镜像：npm config set registry https://registry.npm.taobao.org
>
> 注意：该配置只需在第一次安装时使用即可。



#### 创建项目

> 安装脚手架后，会生成一新的命令vue

1. 进入指定项目根目录，执行下列命令

`vue create 项目名称`

![image-20220503113312047](F:\study_notes\前端\vue_notes\vue-cli的基本使用.assets\image-20220503113312047.png)

2. 接下来需要选择vue版本号，按下回车，vue开始编译创建项目至指定路径。
3. 创建完毕后，根据提示，启动项目即可。
                                                            ![image-20220503113506908](F:\study_notes\前端\vue_notes\image-20220503113506908.png) 





## 项目文件夹说明：

main.js

![image-20220503141857720](F:\study_notes\前端\vue_notes\vue-cli的基本使用.assets\image-20220503141857720.png)

> 这里挂载也可以不用$mount，使用el挂载一样可以。



App.vue是所有组件的父组件



assets文件夹：存储所有静态资源



components文件夹：所有的组件都存放在这个文件夹下（APP.vue除外）



public下的index.html

![image-20220503120836689](F:\study_notes\前端\vue_notes\vue-cli的基本使用.assets\image-20220503120836689.png)



其他基本配置文件

![image-20220503120957152](F:\study_notes\前端\vue_notes\vue-cli的基本使用.assets\image-20220503120957152.png)



## 关于不同版本的vue

- vue.js与vue.runtime.xxx.js的区别：

  1. vue.js是完整版的 vue，包含：核心功能+模板解析器。
  2. vue.runtime.xxx.js是运行版的vue，只包含：核心功能，没有模板解析器。

- 因为 vue.runtime.xxx.js没有模板解析器，所有不能使用template配置项，需要使用render函数接收到的createElement函数去指定具体内容。

  > 其他地方的template标签，有相应的配置项，见package.json



## vue.config.js配置文件

使用`vue inspect > output.js` 可以查看到vue脚手架的默认配置。

使用`vue.config.js`可以对脚手架进行个性化定制
