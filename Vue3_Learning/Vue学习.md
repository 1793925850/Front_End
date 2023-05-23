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