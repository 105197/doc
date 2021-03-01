# vue-property-decorator

## 简介

使用ts的趋势已经越来越普遍

## 组件的使用及对比

### @Component => vue-class-component

用于绑定组件与注册组件
和vue差不多
`@Component({})`

```ts
@Component({TestValue})
```

```js
//VUE 写法
components:{
 TestValue,
}
```

### get => computed

```ts
get handle(){
    console.log('2@@@@2')
    return this.age
}
```

相等于

```js
computed:{
    handle(){
        console.log('22222')
        return this.age
    }
}
```

### @Prop => props

```ts
props: {
    propA: {
      type: Number
    },
    propB: {
      default: 'default value'
    },
    propC: {
      type: [String, Boolean]
    },
  }

```

```ts
@Props(Number)propA!:number
@Props({default})propA!:number
```

* 注意这里的！为一定有值

### @Watch =>watch

与Vue的用法差不多

```ts
watch :{
    name:function(){
        ...
    },
    age:function(){
        ....
    }
    
}
```

```ts
@Watch('name')
function fn(){
    ....
})
@Wacth('age')
function age(){
}
```

### @Emit =>监听与触发

@Emit 转饰的函数执行后，再执行同名字的函数（只是驼峰变成-连接）

```ts
on-save(){
}
@Emit onSave (){
    
}
```

```js
 mounted(){
            this.$on('emit-todo', function(n) {
                console.log(n)
            })

            this.emitTodo('world');
        }

            @Emit()
        emitTodo(n: string){
            console.log('hello');
        }
```

* 还能再`@Emit('sss'）`，则执行转饰函数，则执行指定函数。

`@Emit()`不传参数,那么它触发的事件名就是它所修饰的函数名.
`@Emit(name: string)`,里面传递一个字符串,该字符串为要触发的事件名.
