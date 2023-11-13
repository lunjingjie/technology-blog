不同维度考虑性能优化：

1.CDN

2.懒加载

3.回流和重绘

4.Javascript中优化

- 事件委托（利用冒泡，把子元素的事件委托到父元素）
- 防抖、节流
- 不使用js动画
- 不用js频繁操作dom，可以使用documentFragment节点挂载dom操作

5.图片优化

6.Webpack优化

7.Vue优化

- 路由懒加载

- 合理使用computed和watch

- v-for添加key

- v-for的同时避免使用v-if

- destory时销毁事件：比如addEventListener添加的事件、setTimeout、setInterval、bus.$on绑定的监听事件等

- 第三方插件按需引入

8.React优化

- map循环展示添加key

- 路由懒加载

- 使用scu，memo或者pureComponent避免不必要的渲染

9.白屏优化

