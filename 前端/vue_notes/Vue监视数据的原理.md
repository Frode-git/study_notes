## Vue监视数据的原理

1. vue会监视data中所有层次的数据。
2. 如何监测对象中的数据？
   通过setter实现监视，且要在new Vue 时就要传入要监测的数据。
   - 对象中后追加的属性，Vue默认不做响应式处理
   - 如需给后添加的属性做响应式，请用如下API：
     `Vue.set(target, propertyName/index, value)`或
     `vm.$set(target, propertyName/index, value)`
3. 如何监测数组中的数据？
   通过包裹数组更新元素的方法实现，本质就是做了两件事：
   - 调用原生对应的方法对数组进行更新。
   - 重新解析模板，进而更新页面。
4. 在Vue修改数组中的某个元素一定要用如下方法：
   - 使用这些API：`push()、pop()、shift()、unshift()、splice()、sort()、reverse()`
   - `Vue.set()`或`vm.$set()`

> 特别注意：`Vue.set()`和`vm.$set()`不能给vm或vm的根数据对象添加属性！！
>
> vm即vm本身，vm的根数据指vm._data



## 数据代理、数据劫持

vue实现对数据的监视，主要用到的就是数据代理和数据劫持，数据代理，就是将data中的数据代理到vm本身，例如：

![image-20220430223528023](F:\study_notes\前端\vue_notes\Untitled.assets\image-20220430223528023.png)![image-20220430223531208](F:\study_notes\前端\vue_notes\Untitled.assets\image-20220430223531208.png)![image-20220430223532611](F:\study_notes\前端\vue_notes\Untitled.assets\image-20220430223532611.png)

data中的数据，在控制台输出vm，可以看到person在vm本身出现了，并且有get person和set person两个方法，vue就是通过这样的数据代理进行数据监视的，同时，我们发现，vue还将data中的数据进行的一些处理（数据劫持）：

![image-20220430223709853](F:\study_notes\前端\vue_notes\Untitled.assets\image-20220430223709853.png)

在vm本身data显示的是_data，这也是一个数据代理。

数据劫持：在这里体现在这个_data，点击 _data，发现跟data里的数据咋不一样呢？

![image-20220430224249918](F:\study_notes\前端\vue_notes\Untitled.assets\image-20220430224249918.png)

这种将上面data中的数据改变成下面这种，遍历data对象的属性，把每个属性都改成一个带有getter和setter的现象（操作），就叫做数据劫持