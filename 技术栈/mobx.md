# mobx轻量状态管理器

## 简介

作为`redux`的替代方案，一般来说在处理复杂度比较高的时候使用`redux`是比较好一些的的,因此`state`会被约束，缺少一些灵活度;，但是一般情况下，灵活性更高，成本更低的`mobx`会比较适合，而且`mobx`是偏向于对象编程
![4fb0f69882fe46035b6c9914aeb3e2fb.png](evernotecid://1FEFC25A-2DF3-4B0C-9965-92FEAC312BEF/appyinxiangcom/30097437/ENResource/p93)

## 核心API

* `observable`
* `action`
* `computed`
* `reaction`
* `autorun`
  
### observable

`observable` 一般用于包装`state`，创建初始化

```ts
 
 class Person{
 @observable name='张三'
 @observable age='22'
 }
 
 
 const Person=({
     name='张三'
     age='22'
 })
 
  const Person=observable([{
     name='张三'
     age='22'
 }])
 
 const list=observable([1,2,34,6])
 
 const map = observable.map({ key: "value" })
 map.set("key", "new value")

const temperature = observable.box(20)
temperature.set(25)

```

### observer 观察者组件

 ```ts
 @observer
 class ss extend react.Compoent{ 
 }
 const timer=observer(()=>{
    //doSomeThing
 })
 
 ```

### computed

用于计算属性，监听`state`属性，一旦`computed`创建的监听函数中的`state`属性发生变化，则会执行相应的函数。在`computed`依赖`state`值不发生变化时，`computed`会处于一个暂停状态，就不会被`observable`,那么会被mobx进行垃圾回收

```ts
import { decorate, observable, computed } from "mobx"

class OrderLine {
    price = 0
    amount = 1

    constructor(price) {
        this.price = price
    }

    get total() {
        return this.price * this.amount
    }
}
decorate(OrderLine, {
    price: observable,
    amount: observable,
    total: computed,
})
```

```ts
import { observable, computed } from "mobx"

class OrderLine {
    @observable price = 0
    @observable amount = 1

    constructor(price) {
        this.price = price
    }

    @computed get total() {
        return this.price * this.amount
    }
}
```

### autorun

工作机制和计算属性差不多，但是相对`computed`来说，`autorun`在依赖state不发生变化时,`autorun`也不会执行函数，但是也不会被回收回去。利用这样的特性，适合于打印日志，更新UI

### action

在`mobx`中唯一可以修改`state`的一个`api`。

### reaction

## 语法

可用类创建，函数方法。类模式可以使用装饰器来进行`@observable`创建，而函数变量则`observable`关键词
