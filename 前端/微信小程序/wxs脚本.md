# wxs--基本概念

## wxs

WXS是小程序独有的一套脚本语言，结合WXML，可以构建出页面的结构。

## wxs的应用场景

wxml中无法调用在页面的.js中定义的函数，但是，wxml中可以调用wxs中定义的函数。因此，小程序中wxs的典型应用场景就是“过滤器”。



## wxs和JavaScript的关系

虽然wxs的语法类似于JavaScript，但是两者是完全不同的语言

1. wxs有自己的数据类型
   - number、string、boolean、object
   - function、array、date、regexp（正则）
2. wxs不支持类似于ES6及以上的语法形式
   - 不支持：let、const、解构赋值、展开运算符、箭头函数、对象属性简写等等
   - 支持：var定义变量、普通function函数类似于ES5的语法
3. wxs遵循CommonJs规范
   - module对象
   - require（）函数
   - module.exports对象

# wxs脚本--基础语法

## 内嵌wxs脚本

wxs代码可以编写在wxml文件中的`<wxs>`标签内，就像JavaScript代码可以边写在html文件中的`<script>`标签内一样。

wxml文件中的每个`<wxs></wxs>`标签，必须提供module属性，用来指定当前wxs的模块名称，方便在wxml中访问模块中的成员

## 使用外联的wxs脚本

在wxml中引入外联的wxs脚本时，必须为<wxs>标签添加module和src属性，其中：

- module用来指定模块的名称
- src永安里指定要引入的脚本的路径，必须是相对路径。



# wxs的特点

1. wxs典型的应用场景就是“过滤器”，经常配合Mustache语法进行使用，但是，在wxs中定义的函数不能作为组件的事件回调函数，例如（错误写法）：

   ```html
   <button bindtap="m1.toLower">按钮</button>
   
   ```

2. 隔离性，隔离性指的是wxs的运行环境和其他JavaScript代码是隔离的。体现在：

   - wxs不能调用js中定义的函数
   - wxs不能调用小程序提供的API

3. 性能好，在IOS设备上，小程序内的wxs会比JavaScript代码快2~20倍，但在Android设备上，无差异