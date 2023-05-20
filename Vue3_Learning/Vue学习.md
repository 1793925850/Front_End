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

