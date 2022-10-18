##### vue2.x响应式原理

依赖收集流程：

1.vue的mount过程，通过mountComponent函数new Watcher();

2.new Watcher()过程中会执行this.get()方法;

3.Watcher的get方法中执行Dep类中的pushTarget方法，把当前Watcher赋值到Dep.target;

4.然后继续执行Watch类的get方法中的value = this.getter.call(vm, vm)，即执行updateComponent（new Watcher()的第二个参数）;

5.updateComponent实际就是执行vm.\_update(vm._render(), hydrating);

6.接着执行vm.render()方法，生成渲染VNode，渲染过程会读取vm上的数据，从而触发数据对象的getter;

7.Object.defineProperty()的getter中，每个getter会持有一个dep，触发时会调用dep.depend()方法，也就是Dep.target.addDep(this)，把Watcher实例放到Dep的subs中;

8.依赖收集完后，Dep.target = targetStack.pop()，恢复成一个状态;

9.this.cleanupDeps()，依赖清空（场景v-if，避免性能浪费）



派发更新原理：

1.在组件中对响应的数据做了修改，触发setter逻辑，调用dep.notify()；

2.dep.notify()中遍历所有的Watcher实例，调用Watcher实例的update方法；

3.执行queueWatcher()，把watcher先添加到一个队列里，然后再nextTick后执行flushSchedulerQueue；

4.flushSchedulerQueue进行队列排序、队列遍历、状态恢复

队列排序：组件更新父优先于子，自定义watcher优先于渲染watcher

队列遍历：执行watcher.run()

状态恢复：把这些控制流程状态的一些变量恢复到初始值，把 watcher 队列清空