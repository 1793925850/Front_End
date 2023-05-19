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

