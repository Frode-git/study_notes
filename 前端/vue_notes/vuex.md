## vuex

### 1.概念

在vue中实现集中式状态（数据）管理的一个**vue插件**，对vue应用中多个组件的共享状态进行集中式的管理（读/写），也是一种组件间通信的方式，且适用于任意组件间通信。
![image-20220507181245408](F:\study_notes\前端\vue_notes\vuex.assets\image-20220507181245408.png)



### 2.何时使用？

多个组件需要共享数据时。

### 3.搭建vuex环境

1. 创建文件：`src/store/index.js`

   > 说明：这里需要注意一下import导入的问题，对于插件的应用，我们一般在main.js中导入，然后调用`Vue.use(xxx)`命令使用，但是vuex的使用，必须先导入`import Vuex from 'vuex'`并使用插件后`Vue.use(Vuex)`，才能导入store`import store from 'xxx/store/index'`，但是脚手架环境下，会搜索全部的import，全部移动到代码最前面（最先执行），于是就会产生一个报错（因为先导入store然后再执行`Vue.use(Vuex)`）

   ```javascript
   // 引入Vue核心库
   import Vue from 'vue'
   // 引入vuex
   import Vuex from 'vuex'
   // 应用vuex插件
   Vue.use(Vuex)
   
   // 准备actions对象 -- 响应组件中用户的动作
   const actions = {}
   // 准备mutations对象 -- 修改state中的数据
   const mutations = {}
   // 准备state对象 -- 保存具体的数据
   const state = {}
   
   // 创建并暴露store
   export default new Vuex.Store({
       actions,
       mutations,
       state
   })
   ```

2. 在`main.js`中创建vm时传入`store`配置项

   ```javascript
   ...
   // 引用store
   import store from './store'
   ...
   
   // 创建vm
   new Vue({
       el: '#app',
       render: h => h(App),
       store
   })
   ```



### 4.基本使用

1. 初始化数据、配置`actions`、配置`mutations`，操作文件`store.js`

   > 所谓配置`actions`、配置`mutations`，就是在actions和mutations中分别写各自的业务行为

2. 组件中读取vuex中的数据: `this.$store.state.xxx`

   > store在vc实例对象上，通过this.$store即可获取到

3. 组件中修改vuex中的数据：`this.$store.dispatch('actions中的方法名', 数据)` 或 `this.$store.commit('mutations中的方法名', 数据)`

   > 若没有网络请求或其他业务逻辑，组件中也可以越过actions，即不写dispatch，直接写commit



### 5.getters的使用

1. 概念：当state中的数据需要经过加工后使用时，可以使用getters加工。

2. 在`store.js`中追加`getters`配置

   ```javascript
   ...
   const getters = {
       deal (state) { // getters中的方法能接受到一个参数，就是state
           return state.sum * 10 // 注意写返回值
       }
   }
   ...
   // 创建并暴露store
   export default new Vuex.Store({
   	...
   	getters
   })
   ```

3. 组件中读取数据：`this.$store.getters.deal`

> getters有点类似计算属性



### 6.四个map方法的使用

1. **mapState**方法：用于帮助我们映射state中的数据为计算属性

   ```javascript
   computed: {
       // 借助mapState生成计算属性（对象写法）
       ...mapState({
           sum: 'sum',
           school: 'school'
       }),
           
       // 借助mapState生成计算属性（数组写法）
       ...mapState(['sum', 'school'])
   }
   ```

   > 这里用展开运算符，是因为mapState方法返回的是一个对象，而计算属性本身就是一个对象。
   >
   > 采用数组写法，表示生成的计算属性名和要从state中获取的数据的名一致

2. **mapGetters**方法：用于帮助我们映射getters中的数据为计算属性

   ```javascript
   computed: {
       // 借助mapGetters生成计算属性（对象写法）
       ...mapGetters({
           sum: 'sum'
       })
       
       // 借助mapGetters生成计算属性（数组写法）
       ...mapGetters(['sum'])
   }
   ```

3. **mapActions**方法：用于帮助我们生成与actions对话的方法，即：包含`this.$store.dispatch(xxx)`的函数

   ```javascript
   methods: {
       // 借助mapActions生成: sum（对象写法）
       ...mapActions({
           sum: 'sum'
       })
       
       // 借助mapActions生成: sum（数组写法）
       ...mapActions(['sum'])
   }
   ```

4. **mapMutations**方法：用于帮助我们生成与mutations对话的方法，即：包含`this.$store.commit(xxx)`的函数

   ```javascript
   methods: {
       // 借助mapMutations生成: sum（对象写法）
       ...mapMutations({
           sum: 'sum'
       })
       
       // 借助mapMutations生成: sum（数组写法）
       ...mapActions(['sum'])
   }
   ```

> 注意：mapActions和mapMutations使用时，若需要传递参数，则要在模板中绑定事件时传递参数，否则参数是事件对象。
>
> 这四个map方法需要从vuex中导入
>
> `import {mapState, mapGetters, mapActions, mapMutations} from 'vuex'`



### 7.模块化+命名空间

1. 目的：让代码更好维护，让多种数据分类更加明确。

2. 修改`store/index.js`

   ```javascript
   const countAbout = {
       namespace: true, // 开启命名空间
       state: {},
       mutations: {},
       actions: {},
       getters: {}
   }
   
   const personAbout = {
       namespace: true, // 开启命名空间
       state: {},
       mutations: {},
       actions: {},
       getters: {}  
   }
   
   const store = new Vuex.Store({
       modules: {
           countAbout,
           personAbout
       }
   })
   ```

   > 这里还可以继续拆分，countAbout和personAbout继续拆，分别放入不同的js文件中，然后暴露出来，在index.js中导入

3. 开启命名空间后，组件中读取state数据：

   ```javascript
   // 方式一： 自己直接读取：
   this.$store.state.personAbout.list
   // 方式二： 借助mapState读取：
   mapState('personAbout', ['list'])
   ```

4. 开启名命名空间后，组件中读取getter数据：

   ```javascript
   // 方式一： 自己直接读取：
   this.$store.getters['personAbout/list']
   // 方式二： 借助mapGetters读取：
   mapGetters('personAbout', ['list'])
   ```

5. 开启名命名空间后，组件中调用dispatch

   ```javascript
   // 方式一： 自己直接dispatch：
   this.$store.dispatch('personAbout/addPerson', person)
   // 方式二： 借助mapActions读取：
   mapActions('personAbout', ['add'])
   ```

6. 开启名命名空间后，组件中调用commit：

   ```javascript
   // 方式一： 自己直接commit：
   this.$store.commit('personAbout/ADD_PERSON', person)
   // 方式二： 借助mapMutations读取：
   mapMutations('personAbout', ['ADD_PERSON'])
   ```

   

### 版本问题

脚手架安装vue时，默认安装vue3版本，所以对于vuex的安装，会安装最新版4（截止笔记目前），而vue2的项目，只能使用3版本的vuex。

安装的时候声明版本号即可。`npm i vuex@3`





