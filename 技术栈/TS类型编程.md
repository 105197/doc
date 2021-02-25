# 基本类型

## 数组

* `string[]` 等价于 `['a','b','c']`
* `number[]`
* `Array<number>`
* `any[]`
* `[index:number]: number`; 
* 类型[]      `string[]`
* 使用通用数组类型`Array<elemType>：Array<string>`
  
## 元组

类似和数组一样，但是已经已知元素的类型和数量

```ts
let arr1:[number,string]=[1,'222'] //ok
let arr2:[number,string]=[1,'222',3] //error
let arr3:[number,string]=['1','222'] //error
```

## 枚举

 以enum，枚举名以大写定义，属性为大写。
 在枚举中，可初始化，当初始化为数字(或者默认)，会执行根据索引值去查询属性值(默认时索引值从0开始)。不然不能使用索引值查询到。一旦使用字符串类型，则所有的枚举属性都要初始化。

 ```ts
 enum Color{
    red，
    yellow
 }
 enum Color{
    red=1, // 1
    yellow // 2
 }
 必须全部为字符串
  enum Color{
    red='1', // '1'
    yellow='2' // '2'
 }
 
 let color:Color=Color.red //0/1/'1'
 let color:Color=Color[1] //yellow/red/error
```

## 类型断言

 类型断言是手动指定变量为一个类型选择，告诉编译器该变量是什么类型，可以执行该类型的方法，但是不是重构该变量。
* 值 as 类型    `(value as string).length`
* <类型>值      `<string>value.length`
  
```ts
 let someValue: unknown = "this is a string";

let strLength: number = (someValue as string).length;
//
let strLength:number = <string>someValue.length
```

## 接口

定义属性的类型，

```ts
interface SquareConfig {
  readOnly name:string
  color?: string;
  width?: number;
  [propName: string]: any;
}
 
interface Shape {
  color: string;
}

interface Square extends Shape {
  sideLength: number;
}

interface Square extends Shape, PenStroke {
  sideLength: number;
}

let square = {} as Square;
square.color = "blue";
square.sideLength = 10;
```

## 类

* `public` ,`private`,`protected`修饰符
* `public` 即为默认值，
* `protected` 不被类外部访问，可以在本类和子类中访问
* `private` 只能在本类访问
* `static` 静态属性 只是类本身上面的属性而不是实例化,实例化是在实例时初始化建立的属性

```ts
class Grid{
    static name='xiaoming'
    name1='xinxioaming'
}
Grid.name                  静态属性
let aaa=new Grid()
aaa.name1  /// xinxioaming   实例化
```

* abstract 抽象属性
抽象类做为其它派生类的基类使用，在父类定义

## 函数类型

* 函数类型包含两个类型一个为输入类型一个为输出类型。
在`=>`左边为输入类型，右边为输出类型

```ts
let myAdd: (baseValue: number, increment: number) => number =
    function(x: number, y: number): number { return x + y; };

===
let myAdd: (baseValue: number, increment: number) :number {return x + y; };
```

* 剩余参数

```ts
function buildName(firstName: string, ...restOfName: string[]) {
  return firstName + " " + restOfName.join(" ");
}

let buildNameFun: (fname: string, ...rest: string[]) => string = buildName;
```

* 重载与this

## 泛型

语法 : <类型变量名> 一般是单字母大写

* `<T>`属性
* 泛型函数
  
```ts
function f9<T>(value:T) : T {
    //传入参数类型为T，返回值的类型也为T
    console.log(`我传入了${value}`)
    return value
}
 
f9<number>(10)

```

* 泛系类
  
```ts
class Ni <T> {
    name : T
    constructor (name : T) {
        this.name = name
    }
    say (value : T) : any {
 
        return `${this.name}说${value}`
    }
}
 
const ni1 = new Ni<string>('ljy')//实例化类，指定类的类型是string
console.log(ni1.say('你好'))
```

* 泛型接口
* 第一种
  
```ts
interface Niniubi {
    <T> (value:T) : any
}
 
let fff : Niniubi = <T>(value : T) : any => {
    return `我传入了${value}`
}
console.log(fff<number>(25))
console.log(fff<string>('ljy'))

```

* 第二种
  
```ts
interface ConfigFnTwo<T>{
    (value:T):T;
}
function setDataTwo<T>(value:T):T{
    return value
}
var setDataTwoFn:ConfigFnTwo<string> = setDataTwo
setDataTwoFn('name');


```

```ts
function add<T>(name:T):T{
}
let out =add<string>('heklo')
或者a
let put = add('heljj)
```

### keyof

TypeScript 允许我们遍历某种类型的属性，并通过 keyof 操作符提取其属性的名称

* 操作接口

```ts
interface Person {
  name: string;
  age: number;
  location: string;
}

type K1 = keyof Person; // "name" | "age" | "location"
type K2 = keyof Person[];  // number | "length" | "push" | "concat" | ...
type K3 = keyof { [x: string]: Person };  // string | number
```

* 操作类

```ts
class Person {
  name: string = "Semlinker";
}

let sname: keyof Person;
sname = "name";
```

* 泛型与约束
  
```ts
type Todo = {
  id: number;
  text: string;
  done: boolean;
}

const todo: Todo = {
  id: 1,
  text: "Learn TypeScript keyof",
  done: false
}

function prop<T extends object, K extends keyof T>(obj: T, key: K) : T[k] {
  return obj[key];
}

const id = prop(todo, "id"); // const id: number
const text = prop(todo, "text"); // const text: string
const done = prop(todo, "done"); // const done: boolean
```

## declare

声明文件一般分为 全局声明与模版声明
`declare var hhh:string`
在别的文件也可以用到并且修改。

### type和interface区别

### 相同点

* 都可以描述属性与方法
* 都可以进行扩展

```ts
interface extends interface (接口继承接口)
type extends type (类型继承类型)
interface extends type (接口继承类型)
 type extends interface (类型继承接口)
```

* `React.FC<PropsType>` 意味着一个组件，所以创建组件时要大写（Test1） !p85)
* `const [state,Setstate]=useState(initValue)`
* `useMemo` 依赖一个参数进行一段逻辑处理，返回的是属性，但是不是有一些副作用的逻辑处理（比如异步请求
* `useCallback`和`useMemo`原理差不多，但是返回的是函数
  
* `useEffect` 相当于`componentDidMount`执行异步操作，有副作用

* `useEffect hook` 看做`componentDidMount`、`componentDidUpdate`、`componentWillUnMount`联合
  
## class 与interface区别

interface 定义属性和方法，但是只是类型没有具体实现，但是class 有具体实现方法

## extends 与implement区别

extends 只要类不是申明为final与abstract就能继承
而与implement 用来实现接口，也可以实现多个接口

* 类型兼容性
* 变量时
x赋予给y时，x定义的变量在y中可以找到，
* 函数时
参数可以少给，返回值要多返
* 类时

只对比结构，赋予的类要在对方的子类中。

* 泛型的兼容性
在泛型接口为空没用到时，可以兼容
在泛型接口已用到时，不可以兼容

```ts
interface Test<T>{
}
let x:Test<string>
let y:Test<number>
x=y
interface Test<T>{
    data:T
}
let x:Test<string>
let y:Test<number>
x!=y

```

## 枚举兼容性

枚举可与数字兼容，但是不同枚举之间的类型不能兼容

### 为什么用Hook

* Hook 与class的区别
* class 的组件之间的服用逻辑复杂
* HOOK可以拆分成更小的函数，达到高复用，解决代码沉宇
* class 的this工作方式与不能忘记双向绑定
* 而react比较偏向函数式，
React.createClass、ES6 classes 和无状态函数（stateless function）
头两个机会每一次调用创建实例，但是无状态创建的只保存一个实例，减低了内存的分配和检查，但是纯函数没有生命周期，所以出现了两者都比较好的优点，hook

* 实现单张图片下载方法
 1、利用a标签进行一个元素绑定，

```ts
 const a=document.createElement('a')
 a.setAttribute('download','图片名称')
 a.herf=url
 document.body.appendChild(link)
 a.click()
```

 2、利用canvas进行Fetch,转换64位

```ts
 function downloadImage(url:string,name:string){
    const image=new Image()
     // 解决跨域 Canvas 污染问题
    image.setAttribute('crossOrigin', 'anonymous')
     image.onload = function() {
          let canvas =document.createElement('canvas')
          canvas.width = image.width
          canvas.height = image.height
          let context: any = canvas.getContext('2d')
     context.drawImage(image, 0, 0, image.width,image.height)
      let _dataURL = canvas.toDataURL('image/jpeg') 
      //得到图片的base64编码数据
      let blob_ = dataURLtoBlob(_dataURL)
// 用到Blob是因为图片文件过大时，在一部风浏览器上会下载失败，而Blob就不会

     let url = {
        name: name || '图片.jpeg', // 图片名称不需要加.png后缀名
       src: blob_,
                }

                let link = document.createElement('a')
                link.setAttribute('href', window.URL.createObjectURL(url.src))
                link.setAttribute('download', url.name)
                document.body.appendChild(link)
                link.click()
            }

            image.src = imgSrc

            function dataURLtoBlob(dataUrl: any) {
                let arr = dataUrl.split(',')
                let mime = arr[0].match(/:(.*?);/)[1]
                let bStr = atob(arr[1])
                let n = bStr.length
                let u8arr = new Uint8Array(n)
                while (n--) {
                    u8arr[n] = bStr.charCodeAt(n)
                }
                return new Blob([u8arr], { type: mime })
            }
 }
```

## 装饰器

* 类装饰器
    类装饰器 如果要返回一个新的构造函数（就是闭包），要处理好
    可以为类通过原型去扩展元素，方法。
* 方法装饰器 三个参数
* 属性装饰器 两个参数
    对于静态成员来说是类的构造函数，对于实例成员来说是类的原型对象；
    成员的名字；
    成员的属性描述符；
* 方法参数装饰器
    对于静态成员来说是类的构造函数，对于实例成员来说是类的原型对象；
    方法名称，如果装饰的是构造函数的参数，则值为undefined
    参数在函数参数列表中的索引；

### 装饰器执行顺序

属性装饰器 > 方法装饰器 > 参数装饰器 > 类装饰器
https://www.jianshu.com/p/f4c961cbb074

### 异步请求一点问题

在`useEffect`中使用异步请求数据时更新state时，会提示在挂载的时候不能更新state的警告，所以在`useEffect`中利用`return`(即是挂载时做的回调)，设置变量为`null`

```ts
useEffect(()=>{
    const test1=async function()=>{
          //修改state
    }
    test1()
    return()=>{test1=null}
},[page])
```

## 断言

* `typeOf`
判断一些属性的类型，`number`,`function`,`object`,`undefined`,`null`，`string`
但是也有缺点，不能准确的判断，有些会返回`object`

* `instanceOf`
判断一个属性是否属于是某个的实例对象，即是判断是否由另一个来构造，但在类型中，比如判断某个属性是否是一个接口内的，但是要知道，接口并不是一个真实的类，在编译的时候会被删除。

* `as`
断言只有一个规则，只要类型中存在一样的属性（方法）时，都可以兼容对方(可以用继承来说明)，虽然ts编译的时候不会报错，但如果传入的值没有断言后的属性，则会报错。