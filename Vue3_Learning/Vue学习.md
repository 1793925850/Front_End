# 01_为什么选择Vue框架

## 1. Vue是什么

渐进式 JavaScript 框架，易学易用，性能出色，适用场景丰富的 Web 前端框架。

## 2. 为什么要学Vue

1. 目前前端最火的框架之一；
2. 目前企业技术栈中要求的知识点；
3. 可以提升开发体验。

# 02_Vue简介

Vue 基于标准 HTML、CSS 和 JavaScript 构建，并提供了一套声明式的、组件化的编程模型，帮助你高效地开发用户界面。无论是简单还是复杂的界面，Vue 都可以胜任。

## 1. 渐进式框架

Vue 是一个框架，也是一个生态

Vue 的设计注重灵活性，和“可以被逐步集成”这个特点。

根据不同的需求场景，可以用不同的方式使用 Vue：

- 无需构建步骤，渐进式增强静态的 HTML；
- 在任何页面中作为 Web Components 嵌入；
- 单页应用（SPA）；
- 全栈/服务端渲染（SSR）；
- Jamstack/静态站点生成（SSG）；
- 开发桌面端、移动端、WebGL，甚至是命令行终端中的界面。

## 2. Vue 官方文档

>中文文档：https://cn.vuejs.org/
>
>英文文档：https://vuejs.org/

# 03_Vue API 风格

Vue 的组件可以按两种不同的风格书写：**选项式 API** 和**组合式 API**。

## 1. 选项式 API

使用选项式 API，我们可以用包含多个选项的对象来描述组件的逻辑，例如 data、methods 和 mounted。选项所定义的属性都会暴露在函数内部的 this 上，它会指向当前的组件实例。如下所示：

```vue
<script>
export default {
    data(){
        return {
            count: 0
        }
    },
    methods: {
        increment(){
            this.count++
        }
    },
    mounted(){
        console.log(`The initial count is ${this.count}.`)
    }
}
</script>

<template>
	<button @click="increment">
        Count is: {{ count }}
    </button>
</template>
```

## 2. 组合式 API

通过组合式 API，我们可以使用导入的 API 函数来描述组件逻辑。

```vue
<script setup>
import { ref, onMounted } from 'vue'
const count = ref(0)
function increment(){
    count.value++
}
onMounted(() => {
    console.log(`The initial count is ${count.value}.`)
})
</script>
<template>
	<button @click="increment">
        Count is: {{ count }}
    </button>
</template>
```

推荐采用`组合式 API + 单文件组件`。

# 04_Vue开发前的准备

查看node版本：

```powershell
node -v
```

创建 Vue 项目：

```powershell
npm init vue@latest
```

也可以使用 pnpm，以及使用 vite 来初始化 Vue 文件

接下来会有些选项，看情况选择。

## 1. 开发环境

推荐的 IDE 配置是 **vscode + Volar** 扩展

# 05_Vue 项目目录结构

```go
.vscode			--- vscode工具的配置文件夹
node_modules	--- Vue项目的运行依赖文件夹
public			--- 资源文件夹（浏览器图标）
src				--- 源码文件夹
.gitignore		--- git忽略文件
index.html		--- HTML入口文件
package.json	--- 信息描述文件
README.md		--- 注释文件
vite.config.js	--- Vue配置文件
```

# 06_模板语法

Vue 使用一种基于 HTML 的模板语法，使我们能够声明式地将其组件实例的数据绑定到呈现的 DOM 上。所有的 Vue 模板都是语法层面合法的 HTML，可以被符合规范的浏览器和 HTML 解析器解析。

## 1. 文本插值

最基本的数据绑定形式是**文本插值**，使用的是“Mustache”语法（双大括号）。

```vue
<template>
	<p>
        {{ msg }}
    </p>
</template>

<script>
export default {
    data(){
        return {
            msg:"神奇的魔法"
        }
    }
}
</script>
```

## 2. 使用 JS 表达式

每个绑定仅支持**单一表达式**，也就是一段能够被求值的 JavaScript 代码。一个简单的判断方法是：是否可以合法地写在 **return** 后面。

```vue
<template>
	<p>
        {{ number + 1 }}
    </p>
	<p>
        {{ ok ? 'YES' : 'NO' }}
    </p>
	<p>
        {{ message.spilt('').reverse().join('') }}
    </p>
</template>

<script>
export default {
    data(){
        return {
            number:10,
            ok:true,
            message:"大家好"
        }
    }
}
</script>
```

也不支持**条件控制**。

## 3. 原始 HTML

双大括号会将数据插值为纯文本，而不是 HTML。若想插入 HTML，需要使用`v-html`指令。

```vue
<template>
	<p>
        纯文本: {{ rawHtml }}
    </p>
	<p>
        属性: <span v-html="rawHtml"></span>
    </p>
</template>

<script>
export default {
    data(){
        return {
            rawHtml:"<a href='https://itbaizhan.com'>百战程序员</a>"
        }
    }
}
</script>
```

# 07_属性绑定

双大括号不能再 HTML attributes 中使用。想要响应式地绑定一个 attribute，应该使用 v-bind 指令。

```vue
<template>
	<div v-bind:id="dynamicId" v-bind:class="dynamicClass">AppID</div>
</template>

<script>
export default {
    data(){
        return {
            dynamicId:"appid",
            dynamicClass:"appclass"
        }
    }
}
</script>
```

`v-bind` 指令指示 Vue 将元素的 `id` attribute 与组件的 `dynamicId` 属性保持一致。

如果绑定的值是 `null` 或者`undefined`，那么该 attribute 将会从渲染的元素上移除。

## 1. 简写

因为 v-bind 非常常用我们提供了特定的简写语法

```vue
<div :id="dynamicId" :class="dynamicClass"></div>
```

## 2. 布尔型 Attribute

![1684594749971](D:\Typora\user-image\1684594749971.png)

## 3. 动态绑定多个值

![1684594916372](D:\Typora\user-image\1684594916372.png)

# 08_条件渲染

在 Vue 中，提供了条件渲染，这类似于 JavaScript 中的条件语句：

- v-if
- v-else
- v-else-if
- v-show

## 1. v-if

v-if 指令用于条件性地渲染一块内容。这块内容只会在指令的表达式返回**真值**时才被渲染。

![1684663387313](D:\Typora\user-image\1684663387313.png)

## 2. v-else

也可以使用 v-else 为 v-if 添加一个“else 区块”

![1684663599657](D:\Typora\user-image\1684663599657.png)

## 3. v-else-if

v-else-if 提供的是相应于 v-if 的“else if 区块”。它可以连续多次重复使用。

```vue
<template>
	<div v-if="type === 'A'">
        A
    </div>
	<div v-else-if="type === 'B'">
        B
    </div>
	<div v-else-if="type === 'C'">
        C
    </div>
	<div v-else>
        Not A/B/C
    </div>
</template>

<script>
export default {
	data(){
		return {
            type:"D"
        }
	}
}
</script>
```

## 4. v-show

另一个可以用来按条件显示一个元素的指令是 v-show（相当于没有 v-else 的 v-if ）。其用法基本一样：

![1684663995261](D:\Typora\user-image\1684663995261.png)

## 5. v-if 和 v-show 的区别

![1684664105471](D:\Typora\user-image\1684664105471.png)

# 09_列表渲染

![1684664324381](D:\Typora\user-image\1684664324381.png)

## 1. 复杂数据

大多数情况下，渲染的数据源来源于网络请求，也就是 JSON 格式。

![1684664531166](D:\Typora\user-image\1684664531166.png)

v-for 也支持使用可选的第二个参数表示当前项的**位置索引**。

![1684664838558](D:\Typora\user-image\1684664838558.png)

也可以使用 of 作为分隔符来替代 in，这更接近 JavaScript 的迭代器语法。

```vue
<div v-for="item of items">
    
</div>
```

## 2. v-for 与对象

可以使用 v-for 来遍历一个对象的所有属性

![1684665000446](D:\Typora\user-image\1684665000446.png)

# 10_通过 key 管理状态

![1684665249227](D:\Typora\user-image\1684665249227.png)

![1684665515440](D:\Typora\user-image\1684665515440.png)



>**PS：**
>
>key 在这里是一个通过 v-bind 绑定的特殊 attribute
>
>推荐在任何可行的时候为 v-for 提供一个 key attribute
>
>key 绑定的值期望是一个基础类型的值，例如 string 或 number 类型

## 1. key 的来源

不建议使用 index 作为 key 的值，因为我们要确保每一条数据的唯一索引不会发生变化。

![1684665750164](D:\Typora\user-image\1684665750164.png)

可以使用对象里面的 id 属性作为 key 的值

# 11_事件处理

我们可以使用 v-on 指令（简写为 @ ）来监听 DOM 事件，并在事件触发时执行对应的 JavaScript。用法：v-on:click=“methodName”或@click=“handler”。

事件处理器的值可以是：

- **内联事件处理器：**事件被触发时执行的内联 JavaScript 语句（与 onclick 类似）
- **方法事件处理器：**一个指向组件上定义的方法的属性名或是路径

## 1. 内联事件处理器

内联事件处理器通常用于`简单场景`。

```vue
<template>
	<button @click="count++">
        Add 1
    </button>
	<p>
        Count is: {{ count }}
    </p>
</template>

<script>
export default {
	data(){
		return {
            count:0
        }
	}
}
</script>
```

## 2. 方法事件处理器

工作中主要用到的。

```vue
<template>
	<button @click="addCount">
        Add
    </button>
	<p>
        Count is: {{ count }}
    </p>
</template>

<script>
export default {
	data(){
		return {
            count:0
        }
	},
    
    // methods 所有的方法或函数都放在这里
    methods:{
        addCount(){
            // 读取到 data 里面的数据的方案：this.count
            this.count++
        }
    }
}
</script>
```

# 12_事件传参

事件参数可以获取 event 对象和通过事件传递数据。

## 1. 获取 event 对象

![1684667336967](D:\Typora\user-image\1684667336967.png)

Vue 中的 event 对象，就是原生 JS 的Event 对象。

## 2. 传递参数

![1684667569056](D:\Typora\user-image\1684667569056.png)

## 3. 传递参数过程中获取 event 对象

![1684667610545](D:\Typora\user-image\1684667610545.png)

# 13_事件修饰符

![1684667718869](D:\Typora\user-image\1684667718869.png)

为了解决这一问题，Vue 为 v-on(@) 提供了**事件修饰符**，常用有以下几个：

- .stop
- .prevent
- .once
- .enter
- 等等

> **具体参考**
>
> 地址：https://cn.vuejs.org/guide/essentials/event-handing.html#event-modifiers

## 1. 阻止默认事件

![1684667973066](D:\Typora\user-image\1684667973066.png)

## 2. 阻止事件冒泡

![1684668380314](D:\Typora\user-image\1684668380314.png)

触发子组件的同时，也触发了父组件，这种事件就叫作“**事件冒泡**”。

# 14_数组变化侦测

## 1. 变更方法

Vue 能够侦听响应式数组的变更方法，并在它们被调用时触发相关的更新。这些变更方法包括：

- push()
- pop()
- shift()
- unshift()
- splice()
- sort()
- reverse()

```vue
<template>
	<div>
        <p v-for="(item, index) in names" :key="index">
            {{ item }}
    	</p>
        <button @click="clickAddNamesHandle">
            增加数据
    	</button>
    </div>
</template>

<script>
export default {
    data(){
        return{
            names:["iaiai", "dosds", "dsdsds"]
        }
    },
    methods:{
        clickAddNamesHandle(){
            this.names.push("sakura")
        }
    }
}
</script>
```

## 2. 替换一个数组

![1684806845541](D:\Typora\user-image\1684806845541.png)

![1684806991765](D:\Typora\user-image\1684806991765.png)

# 15_计算属性

![1684807119474](D:\Typora\user-image\1684807119474.png)

![1684807275126](D:\Typora\user-image\1684807275126.png)

> PS：
>
> 返回的值是不需要加括号的

**计算属性**(computed)就是把模板语法里复杂的属性放在一个函数里

也可以把计算属性的函数放在 methods 里，只不过这就成为方法了，因此要加小括号表示返回值

## 1. 计算属性缓存 vs 方法

**重点区别：**

计算属性：计算属性值会基于其响应式依赖被缓存。一个计算属性仅会在其响应式依赖更新时才重新计算。(惰性)

方法：方法调用总是会在重渲染发生时再次执行函数。

# 16_Class绑定

数据绑定的一个常见需求场景是`操纵元素的 CSS class 列表`，因为 class 是 attribute，因此可以和其它 attribute 一样使用 v-bind 将它们和动态的字符串绑定。

但，在处理比较复杂的绑定时，通过拼接生成字符串是麻烦且易出错的。

因此，Vue 专门为 class 的 v-bind 用法提供了特殊的功能增强。除了字符串外，表达式的值也可以是`对象`或`数组`。

## 1. 绑定对象

![1684807981563](D:\Typora\user-image\1684807981563.png)

## 2. 多个对象绑定

![1684808137920](D:\Typora\user-image\1684808137920.png)

## 3. 绑定数组

![1684808221712](D:\Typora\user-image\1684808221712.png)

如果想在数组中有条件地渲染某个 class，可以使用三元表达式：

```vue
<template>
	<div :class="[isActive ? 'active' : '']">
        isActive
    </div>
</template>

<script>
export default {
    data(){
        return{
            isActive:true
        }
    },
}
</script>
```

## 4. 数组和对象

![1684808469545](D:\Typora\user-image\1684808469545.png)

> **提示**
>
> 数组和对象嵌套过程中，只能是**数组嵌套对象**

# 17_Style绑定

数据绑定的一个常见需求场景是`操纵元素的 CSS style 列表`，因为 class 是 attribute，因此可以和其它 attribute 一样使用 v-bind 将它们和动态的字符串绑定。

但，在处理比较复杂的绑定时，通过拼接生成字符串是麻烦且易出错的。

因此，Vue 专门为 style 的 v-bind 用法提供了特殊的功能增强。除了字符串外，表达式的值也可以是`对象`或`数组`。

## 1. 绑定对象

```vue
<template>
	<div :style="{ color: activeColor, fontSize: fontSize + 'px' }">
        Style绑定
    </div>
</template>

<script>
export default {
    data() {
        return {
            activeColor:'red'
            fontSize: 30
        }
    }
}
</script>
```

![1684809539265](D:\Typora\user-image\1684809539265.png)

## 2. 绑定数组

![1684809584714](D:\Typora\user-image\1684809584714.png)

了解就行，一般没啥意义

# 18_侦听器

**作用：**侦听页面数据的变化。

可以使用 watch 选项在每次响应式属性(也就是双花括号{{}}里的数据)发生变化时触发一个函数。

![1684809833774](D:\Typora\user-image\1684809833774.png)

> 方法名必须与侦听的变量名一致

# 19_表单输入绑定

![1684809964718](D:\Typora\user-image\1684809964718.png)

![1684809987321](D:\Typora\user-image\1684809987321.png)

效果：

![1684810115204](D:\Typora\user-image\1684810115204.png)

## 1. 复选框

![1684810221137](D:\Typora\user-image\1684810221137.png)

## 2. 修饰符

v-model 也提供了修饰符：.lazy、.number、.trim

默认情况下，v-model 会在每次 input 事件后更新数据。

### 2.1. .lazy

可以添加 lazy 修饰符来改为在每次 change 事件后(比如，失去焦点、回车等操作)更新数据。

![1684810545483](D:\Typora\user-image\1684810545483.png)



# 20_模板引用

虽然 Vue 的声明性渲染模型为你抽象了大部分对 DOM 的直接操作，但在某些情况下，我们仍然需要直接访问底层 DOM 元素。要实现这一点，可以使用特殊的 ref attribute。

挂载结束后引用都会被暴露在 this.$refs 之上。

![1684811103380](D:\Typora\user-image\1684811103380.png)



> 如果没有特别的需求，不要操作 DOM

# 21_组件组成

组件最大的优势就是**可复用性**。

当使用构建步骤时，我们一般会将 Vue 组件定义在一个单独的 **.vue** 文件中，这被叫做**单文件组件**(简称 **SFC**)。

## 1. 组件组成结构

```vue
<!--template 承载所有的 html 标签-->
<template>
	<div>
        承载标签
    </div>
</template>

<!--script 承载所有的业务逻辑-->
<script>
export default{}
</script>

<!--style 承载所有的样式-->
<!--scoped 让当前样式只在当前组件中生效-->
<style scoped>
</style>
```

## 2. 组件引用

![1684828578814](D:\Typora\user-image\1684828578814.png)

必须存在 template 标签



# 22_组件嵌套关系

![1684828840267](D:\Typora\user-image\1684828840267.png)

![1684828894935](D:\Typora\user-image\1684828894935.png)



## 1. 创建组件及引用关系

### 1.1. Header

![1684828979248](D:\Typora\user-image\1684828979248.png)

### 1.2. Main

```vue
<template>
  <div class="main">
      <h3>MainVue</h3>
  </div>
</template>

<script>
export default {

}
</script>

<style>
.main{
    float: left;
    width: 70%;
    height: 600px;
    border: 5px solid #999;
    box-sizing: border-box;
}
</style>
```

### 1.3. Aside

```vue
<template>
    <div class="aside">
        <h3>AsideVue</h3>
    </div>
</template>

<script>
export default {

}
</script>

<style scoped>
.aside{
    float: right;
    width: 29%;
    height: 600px;
    border: 5px solid #999;
    box-sizing: border-box;
}
</style>
```

### 1.4. Article

```vue
<template>
  <h3>ArticleVue</h3>
</template>

<script>
export default {}
</script>

<style scoped>
h3{
    width: 80%;
    text-align: center;
    line-height: 100px;
    box-sizing: border-box;
    margin: 50px auto 0;
    background: #999;
}
</style>
```

### 1.5. Item

```vue
<template>
    <h3>ItemVue</h3>
</template>

<script>
export default {}
</script>

<style scoped>
h3{
    width: 80%;
    text-align: center;
    line-height: 100px;
    box-sizing: border-box;
    margin: 10px auto 0;
    background: #999;
}
</style>
```

# 23_组件注册方式

一个 Vue 组件在使用前需要先被“注册”，这样 Vue 才能在渲染模板时找到其对应的实现。组件注册有两种方式：

- 全局注册
- 局部注册

## 1. 全局注册

![1684831574965](D:\Typora\user-image\1684831574965.png)



![1684831672049](D:\Typora\user-image\1684831672049.png)



## 2. 局部注册

全局注册虽然很方便，但有以下几个问题：

- 全局注册，但并没有使用的组件无法在生产打包时被自动移除（也叫“tree-shaking”）。如果你全局注册了一个组件，即使它并没有被实际使用，它仍然会出现在打包后的 JS 文件中
- 全局注册在大型项目中使项目的依赖关系变得不那么明确。在父组件中使用子组件时，不太容易定位子组件的实现。和使用过多的全局变量一样，这可能会影响应用长期的可维护性

局部注册需要使用 components 选项

![1684832031119](D:\Typora\user-image\1684832031119.png)



# 24_组件传递数据 _props

组件与组件之间不是完全独立的，而是有交集的。那就是组件与组件之间是可以**传递数据**的。

传递数据的解决方案就是 props

![1684832177278](D:\Typora\user-image\1684832177278.png)

![1684832374285](D:\Typora\user-image\1684832374285.png)



## 1. 动态传递数据

![1684832552553](D:\Typora\user-image\1684832552553.png)



> **注意事项：**
>
> props 传递数据只能从父级传递到子级



# 25_组件传递多种数据类型

通过 props 传递数据，不仅可以传递字符串类型的数据，还可以是其他类型，例如：数字、对象、数组等。

但实际上**任何**类型的值都可以作为 props 的值被传递。

例如：

![1684832797566](D:\Typora\user-image\1684832797566.png)

# 26_组件传递Props校验

Vue 组件可以更细致地声明对传入的 props 的校验要求。

![1684833086702](D:\Typora\user-image\1684833086702.png)

## 1. 默认值

![1684833230599](D:\Typora\user-image\1684833230599.png)



> 数字和字符串可以直接 default，但是如果是数组和对象，必须通过工厂函数返回默认值。

![1684833403906](D:\Typora\user-image\1684833403906.png)

## 2. 必选项

![1684833455424](D:\Typora\user-image\1684833455424.png)

## Props 是只读的



# 27_组件事件

在组件的模板表达式中，可以直接使用 **$emit** 方法触发自定义事件

触发自定义事件的目的是组件之间传递数据

![1684844952301](D:\Typora\user-image\1684844952301.png)



> **注意：**
>
> 组件之间传递的方案：
>
> - 父传子：props
> - 子传父：自定义事件(this.$emit)



# 28_组合时间配合 v-model 使用

如果是用户输入，我们希望在获取数据的同时发送数据配合 v-model 来使用

![1684845376193](D:\Typora\user-image\1684845376193.png)

![1684845384924](D:\Typora\user-image\1684845384924.png)



# 29_组件数据传递

![1684845425512](D:\Typora\user-image\1684845425512.png)

props 可以传递函数，从而实现子传父（回调函数）



# 30_透传 Attribute

“透传 Attribute”指的是传递给一个组件，却没有被该组件声明为 props 或 emits 的attribute 或者 v-on 事件监听器。最常见的例子是 class、style 和 id。

当一个组件以单个元素为根作渲染时，透传的 attribute 会自动被添加到根元素上。

**限制：**

- 必须是唯一根元素

## 1. 禁用 Attributes 继承

![1684846149656](D:\Typora\user-image\1684846149656.png)

# 31_插槽Slots

组件如何接收模板内容？

模板指的是不在是数据了，而是一个 html 结构，比如一个 div。

在某些场景中，我们可能想要为子组件传递一些模板片段，让子组件在它们的组件中渲染这些片段。

![1684911048113](D:\Typora\user-image\1684911048113.png)

![1684911103970](D:\Typora\user-image\1684911103970.png)



<slot>元素是一个插槽出口(slot outlet)，标示了父元素提供的插槽内容(slot content)将在哪里被渲染。

![1684911244075](D:\Typora\user-image\1684911244075.png)

## 1. 渲染作用域

插槽内容可以访问到父组件的数据作用域，因为插槽内容本身是在父组件模板中定义的。

![1684911387080](D:\Typora\user-image\1684911387080.png)

## 2. 默认内容

在外部没有提供任何内容的情况下，可以为插槽指定默认内容：

```vue
<template>
	<h3>
        ComponentB
    </h3>
	<slot>插槽默认值</slot>
</template>
```

## 3. 具名插槽

通过给插槽添加名字来进行分开渲染。

![1684911936528](D:\Typora\user-image\1684911936528.png)

![1684911973496](D:\Typora\user-image\1684911973496.png)

## 4. 插槽中的数据传递

在某些场景下插槽的内容可能想要同时使用父组件域内和子组件域内的数据。

要做到这一点，需要一种方法来让子组件在渲染时将一部分数据提供给插槽。

可以像对组件传递 props 那样，向一个**插槽的出口**传递 attributes

## 5. 具名插槽的数据传递



# 32_组件生命周期

![1684912623443](D:\Typora\user-image\1684912623443.png)

## 1. 生命周期示意图

![](D:\Typora\user-image\28424bc0ceb5489d87f1f75516bd9101.png)

红色的圆角长方形里面就是生命周期函数，一共有8个生命周期函数

![1684913282418](D:\Typora\user-image\1684913282418.png)



# 33_生命周期应用

两个常用的应用：

- 通过 ref 获取元素 DOM 结构
- 模拟网络请求渲染数据

## 1. 通过 ref 获取元素 DOM 结构

![1684913536501](D:\Typora\user-image\1684913536501.png)

## 2. 模拟网络请求渲染数据

比如在生命钩子函数中进行变量的赋值。



# 34_动态组件

有些场景会需要在两个组件间来回切换，比如 Tab 界面。

## 1. A、B两个组件

![1684914197687](D:\Typora\user-image\1684914197687.png)

加个用来判断以及切换的方法：

![1684914297685](D:\Typora\user-image\1684914297685.png)

赋值一定要字符串

# 35_组件保持存活

![1684914419161](D:\Typora\user-image\1684914419161.png)

![1684914578718](D:\Typora\user-image\1684914578718.png)

# 36_异步组件

在大型项目中，我们可能需要拆分应用为更小的块，并仅在需要时再从服务器加载相关组件。Vue 提供了 `defineAsyncComponent` 方法来实现此功能。

异步组件用于优化项目的性能。优势，打开项目会更快。

![1684914936531](D:\Typora\user-image\1684914936531.png)

# 37_依赖注入

通常情况下，当我们需要从父组件向子组件传递数据时，会使用 props。想象一下这样的结构：有一些多层级嵌套的组件，形成了一棵巨大的组件树，而某个深层的子组件需要一个较远的祖先组件中的部分数据。在这种情况下，如果仅使用 props 则必须将其沿着组件链逐级传递下去，这会非常麻烦。

![1684915087093](D:\Typora\user-image\1684915087093.png)

这一问题被称为“prop 逐级透传”

![1684915117593](D:\Typora\user-image\1684915117593.png)

## 1. provide（提供）

要为组件后代提供数据，需要使用到 provide 选项

```vue
export default {
	provide: {
		message: 'hello!'
	}
}
```

也可以读取 data 中的数据

![1684915512389](D:\Typora\user-image\1684915512389.png)

除了在一个组件中提供依赖，还可以在整个应用层面提供依赖

![1684915574912](D:\Typora\user-image\1684915574912.png)



## 2. inject（注入）

要注入上层组件提供的数据，需使用 inject 选项来声明

![1684915484534](D:\Typora\user-image\1684915484534.png)



> **注意**
>
> provide 和 inject 只能由上到下的传递

# 38_Vue应用

## 1. 应用实例

每个 Vue 应用都是通过 createApp 函数创建一个新的**应用实例**。

```vue
import { createApp } from 'vue'

const app = createApp({
	/* 根组件选项 */
})
```

在一个 Vue 项目中，有且只有一个 Vue 的实例对象

app：Vue 的实例对象



## 2. 根组件

传入 createApp 的对象实际上是一个组件，每个应用都需要一个“根组件”，其他组件将作为其子组件。

![1684916000138](D:\Typora\user-image\1684916000138.png)

## 3. 挂载应用

应用实例必须在调用了 .mount() 方法后才能渲染出来。

该方法接收一个“容器”参数，可以是一个实际的 DOM 元素或是一个 CSS 选择器字符串。

![1684916159800](D:\Typora\user-image\1684916159800.png)

其实真正的运行入口是 index.html 文件。

## 4. 公共资源

在 src 目录下的 assets 文件夹的作用就是存放公共资源，例如：图片、公共CSS或者字体图标等。

![1684916380370](D:\Typora\user-image\1684916380370.png)



vite 就类似于 webpack

