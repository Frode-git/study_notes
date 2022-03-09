## vue-cli 的基本使用

### 安装项目

1. 进入指定项目根目录，打开终端

2. 安装 三脚架  在终端输入命令 `npm install -g @vue/cli  // install可简写为 i` 

3. 安装完毕后，输入命令 `vue -V`  检查是否已装上

4. 在终端输入命令，创建项目

   ```
    vue create 项目名称   // 项目名称最好全英文（不含空格）
   ```

  ![](D:\前端学习\VUEnotes\note_images\01.png)

![<img src="C:\Users\烧鸡公\Desktop\02.png"  />](D:\前端学习\VUEnotes\note_images\02.png)  

> 这里学的 vue2,所以选择了创建 vue2 的项目

![](D:\前端学习\VUEnotes\note_images\03.png) 

![](D:\前端学习\VUEnotes\note_images\04.png) 

![](D:\前端学习\VUEnotes\note_images\05.png) 

![](D:\前端学习\VUEnotes\note_images\06.png)



#### vue 项目中 src 目录的构成：

```
assets 文件夹：存放目录中用到的静态资源文件，例如：CSS 样式表、图片资源
components 文件夹：封装的、可复用的组件，都要放到此目录下
main.js	文件：是整个项目的入口文件，整个项目的运行，要先运行此文件
App.vue 文件：是整个项目的根组件
```





### 更改项目名称

1. 找到根目录下的package.json文件

2. 修改其中的 name 属性，其值为项目名称

3. 删除目录下的 node_modules 文件夹，然后重新安装。

   > 注意：通过npm安装的插件也要全部重新安装

