## 消息订阅与发布

1. 一种组件间通信的方式，适用于任意组件间通信。

2. 使用步骤：

   1. 安装pubsub: `npm i pubsub-js`

      > 订阅与发布的第三方库有很多，这里以pubsub举例

   2. 引入：`import pubsub from 'pubsub-js'`

   3. 接收数据：A组件想接收数据，则在A组件中订阅消息，订阅的回调留在A组件自身。

      ```javascript
      methods: {
          demo(msgName, data) {}
      },
      ...
      mounted() {
          this.pid = pubsub.subscribe('xxx', this.demo) // 订阅消息
          // 注意这里的回调函数this不指向组件实例对象，因此
      }
      ```

   4. 提供数据：`pubsub.publish('xxx', 数据)`

   5. 最好在beforeDestroy钩子中，用`pubsub.unsubscribe(pid)`取消订阅。