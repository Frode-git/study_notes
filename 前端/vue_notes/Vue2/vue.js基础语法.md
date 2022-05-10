## 使用 v-for 取数组中的几个值

> 有些时候，我们只需要渲染数组中的某几个元素，可以使用一下方法
>
> 实例：表示渲染数组中的前四个元素

```vue
<li v-for="(it, index) in list.splice(0, 4)">
	{{ it }}
</li>
```





## 给vue实例（组件实例）绑定新属性

通过`Vue.set(key, value)` 或 `this.$set(key, value)`，不能直接通过`this.key = value`，这样的数据不是响应式的
