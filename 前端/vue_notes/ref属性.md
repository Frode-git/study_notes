## ref属性

在vue中，尽量不要亲自操作DOM元素，但是在某些情况下，需要操作DOM元素，js中可以通过`document.getElementById`获取，vue中提供了更好的方式

给DOM元素绑定ref属性：
`<h1 ref="title">hello</h1>`

通过`this.$refs.title`即可获取

> 这里的this指的是当前组件实例对象



ref属性被用来给元素或子组件注册引用信息（id的替代者），应用在html标签上获取的是真实DOM元素，应用在组件标签上是组件实例对象