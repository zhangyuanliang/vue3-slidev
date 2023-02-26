---
# try also 'default' to start simple
theme: default
colorSchema: light
# random image from a curated Unsplash collection by Anthony
highlighter: shiki
# apply any windi css classes to the current slide
# class: 'text-center'
layout: cover
fonts:
  # 与 css 中的 font-family 一致，你可以使用 `,` 来分割字体名，便于降级
  sans: 'Helvetica Neue,Robot'
  # 将 'Helvetica Neue' 作为本地字体
  local: 'Helvetica Neue'
---

# Vue 3 > Vue 2 + 1
<div class="mt-1 text-xl text-gray-400">2023年2月12日</div>

<style>
h1 {
  background-color: #2B90B6;
  background-image: linear-gradient(315deg,#42d392 25%,#647eff);
  background-size: 100%;
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
</style>

---
layout: 'image-left'
image: '/composition.png'
class: my-cool-content-on-the-right
---

<style>
h1 {
  background-color: #2B90B6;
  background-image: linear-gradient(315deg,#42d392 25%,#647eff);
  background-size: 100%;
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
.my-cool-content-on-the-right {
  padding-top: 2.2rem!important;
  padding-bottom: 0!important;
  background-image: none!important;
}
</style>

# 回顾 vue2 对比 vue3
 
<div v-click="1" class="mt-8">
<div class="mb-4 font-bold">
传统的 vue2 :
</div>

* 逻辑比较分散，代码被强制拆分在了不同的选项中
* 可读性差，需要在文件中反复上下滚动
* 可维护性差

</div>

<div v-click="2" class="mt-4">
<div class="mb-4 font-bold">
  对比 vue3<span class="text-red-500 text-xl">*</span> :
</div>

* 逻辑分明，同一个逻辑关注点相关的代码被归为了一组
* 可读性高，无需在不同的选项块来回滚动切换
* 可维护性好

</div>

<div class="absolute bottom-4 right-3">

<span class="text-gray-400">内容来源：</span>[vue3官网](https://cn.vuejs.org/guide/extras/composition-api-faq.html#more-flexible-code-organization)

</div>

---
layout: section
---

# 开启 Vue3 的世界
## 组合式 API (Composition API) 

---

# Vue3.0 新特性介绍

<div class="flex">
<div class="flex-1">
```html {monaco}
<template>
  <button @click="increment">
    {{ state.count }}
  </button>
  <div>fragment</div>
</template>
<script>
import { reactive } from 'vue'
export default {
  setup() {
    const state = reactive({ count: 0 })
    function increment() {
      state.count++
    }
    // 不要忘记同时暴露 increment 函数
    return {
      state,
      increment
    }
  }
}
</script>
<style></style>
```
</div>

<div class="flex-1 ml-4">

1. 重写双向数据绑定
    * 基于Proxy
2. VDOM性能瓶颈
    * 只对比带有标记的,减少了非动态内容的对比消耗<a class="text-blue-600" href="https://vue-next-template-explorer.netlify.app/#eyJzcmMiOiI8ZGl2PkhlbGxvIFdvcmxkPC9kaXY+XG48ZGl2PkhlbGxvIFdvcmxkPC9kaXY+XG48ZGl2PkhlbGxvIFdvcmxkPC9kaXY+XG48ZGl2PkhlbGxvIFdvcmxkPC9kaXY+XG48ZGl2PkhlbGxvIFdvcmxkPC9kaXY+XG48ZGl2IHYtZm9yPVwiaXQgaW4gWzEsMiwzLDRdXCIgOmtleT1cIml0XCIgOmNsYXNzPVwiYGl0ZW0tJHtpdH1gXCI+e3tpdH19PC9kaXY+Iiwib3B0aW9ucyI6e319">vue-next-template-explorer</a>
3. Fragments
4. Tree-Shaking的支持
    * 全局 API 进行分块。不使用某些功能，它们将不包含在你的基础包中
5. Composition API
    * Setup 语法糖式编程，一会详细讲解

</div>

</div>

---
layout: two-cols
class: vite-project
---
<style>
  .vite-project ul {
    @apply !list-disc;
  }
  .vite-project li::marker {
    @apply inline-block text-vgreen;
  }
</style>
# vue3 + vite 项目目录结构

* public 下面的不会被编译 可以存放静态资源

* assets 可以存放可编译的静态资源

* components 用来存放我们的组件

* App.vue 是全局组件

* main.js 全局的js文件

* index.html 入口文件

* vite.config.js vite的配置文件

::right::

<div class="flex justify-center">

<img src="/vite-project.png" class="w-38 rounded">

<div v-click="1">
<img src="/vite-project-2.png" class="h-100 rounded ml-2">
</div>

</div>

---

# Globale APIs

<div class="flex justify-between">
  <div class="flex-grow mr-2">

```js{all|1|6-8|10|1,6-10}
import Vue from 'vue'
import Dialog from './Dialog.vue'
import ClickOutside from '.clickOutside.js'
import PortalVue from 'portal-vue'

Vue.component('Dialog', Dialog)
Vue.directive('clickOutside', ClickOutside)
Vue.use(PortalVue)

new Vue(App).$mount('#app')
```

  </div>
  <div class="flex-grow">

```js{all|1|6,11|7-10|7-11}
import { createApp } from 'vue'
import Dialog from './Dialog.vue'
import ClickOutside from '.clickOutside.js'
import PortalVue from 'portal-vue'

const app = createApp(App)
app.component('Dialog', Dialog)
app.directive('clickOutside', ClickOutside)
app.use(PortalVue)

app.mount('#app')
```

  </div>
</div>

---

<style>
  .slidev-layout td, .slidev-layout th {
    padding-top: 0.56rem;
    padding-bottom: 0.56rem;
  }
  theader {
    background: #e5e7eb
  }
</style>
# 生命周期

<div class="mt-1"></div>

| 选项式 API | setup语法糖 |
| ------- | ------- |
|    beforeCreate     |    无     |
|    created     |    无     |
|    beforeMount     |    onBeforeMount     |
|    mounted     |    onMounted     |
|    beforeUpdate     |    onBeforeUpdate     |
|    updated     |    onUpdated     |
|    beforeUnmount     |    onBeforeUnmount     |
|    unmounted     |    onUnmounted     |

---
layout: two-cols
class: vite-project
---
# vue3 指令

* v-text
* v-html
* v-show
* v-if
* v-for
* v-on
* v-bind
* v-model
* v-slot
* v-pre
* v-once
* v-memo <Badge type="warn">new</Badge>
* v-cloak

::right::

## v-meno 例子：

```html{all|7|16-21}
<template>
  <div v-memo="[valueA, valueB]">
    <div>{{list}}</div>
  </div>
  <div>{{list}}</div>
  <button @click="add">新增</button>
  <button @click="changeMeno">changeMeno</button>
</template>
<script setup>
  import { ref } from 'vue'

  const valueA = ref(0)
  const valueB = ref(0)
  const list = ref([1, 2, 3, 4, 5])

  function add() {
    list.value = [
      ...list.value,
      ++ list.value.length
    ]
  }
  function changeMeno() {
    ++valueA.value
  }
</script>
```

---

# Vue SFC Playground

<div class="overflow-hidden absolute top-24 left-3 text-center">
  <iframe src="https://sfc.vuejs.org/#eNp9UktugzAQvcrImyYCTL+biERN9j1BnAWBISEFG9mGLhDX6LKLnqCXas9RGxORpmlXtud9Ru/JLVlWFW1qJDMSaSyrIta4YBwgSvMGmqDEUswZWTdxUePSh/5cbRjpSY62aNsiV7rrotC+evV4+4OwrbUWHB6TIk+ezYY4TY3p1+vH5/tbFDr0MjPZx3yHT8iFEYyPE1EUnkSJVCLzSoNCXVe9Y15WQmpoQWIGHWRSlHBlOrhi3MKJ4Eq7oEuYW9LkenoGrC4ANuIwXt/4cOvDnQ/3PjxsDMnSsponOjdRTNbJFFrXoJXR3tSI124GQCkdAf849bwTOi2Q7/TeYRt7dD+2jNWMyzzP5XIOgyYKXUUL4hPXTVDGFT0owc236JVsABQjs6MXI6Yz+2Zkr3WlZmGossR+poOiQu5Cc6Oy5jovkaIqg60ULwqlMWZkiNR7hGbYoAwk8hQlyv88z6i/fIdIHem+Ack79pc="
    width="960"
    height="460"
    class="-mt-14 mb-2"
></iframe>
<a 
class="text-blue-600 underline"
href="https://sfc.vuejs.org/#eNp9UktugzAQvcrImyYCTL+biERN9j1BnAWBISEFG9mGLhDX6LKLnqCXas9RGxORpmlXtud9Ru/JLVlWFW1qJDMSaSyrIta4YBwgSvMGmqDEUswZWTdxUePSh/5cbRjpSY62aNsiV7rrotC+evV4+4OwrbUWHB6TIk+ezYY4TY3p1+vH5/tbFDr0MjPZx3yHT8iFEYyPE1EUnkSJVCLzSoNCXVe9Y15WQmpoQWIGHWRSlHBlOrhi3MKJ4Eq7oEuYW9LkenoGrC4ANuIwXt/4cOvDnQ/3PjxsDMnSsponOjdRTNbJFFrXoJXR3tSI124GQCkdAf849bwTOi2Q7/TeYRt7dD+2jNWMyzzP5XIOgyYKXUUL4hPXTVDGFT0owc236JVsABQjs6MXI6Yz+2Zkr3WlZmGossR+poOiQu5Cc6Oy5jovkaIqg60ULwqlMWZkiNR7hGbYoAwk8hQlyv88z6i/fIdIHem+Ack79pc="
>
sfc.vuejs.org</a>
</div>

---

# 响应式基础

reactive 和 ref

<div class="mt-4 min-h-1"></div>

<div class="flex">
  <div class="flex-grow">

  **声明响应式状态**

  ```html
  <script setup>
  import { reactive } from 'vue'

  const state = reactive({ count: 0 })

  function increment() {
    state.count++
  }
  </script>

  <template>
    <button @click="increment">
      {{ state.count }}
    </button>
  </template>
  ```
  </div>

  <div v-click class="flex-grow mx-2">

  **reactive 的局限性**

  ```js
  const state = reactive({ count: 0 })

  // n 是一个局部变量，同 state.count
  // 失去响应性连接
  let n = state.count
  // 不影响原始的 state
  n++

  // count 也和 state.count 失去了响应性连接
  let { count } = state
  // 不会影响原始的 state
  count++

  // 该函数接收一个普通数字，并且
  // 将无法跟踪 state.count 的变化
  callSomeFunction(state.count)
  ```
  
  </div>

  <div v-click class="flex-grow">

  **用 ref 定义响应式变量**

  ```js
  import { ref } from 'vue'

  const count = ref(0)
  console.log(count) // { value: 0 }
  console.log(count.value) // 0

  count.value++
  console.log(count.value) // 1
  ```
  </div>

</div>

---

# toRef toRefs toRaw

<div class="mt-10 min-h-1"></div>

<div class="flex">
  <div class="flex-grow">
  
  **toRef**

  ```js
  import { reactive, toRef } from 'vue'
 
  const obj = reactive({
    foo: 1,
    bar: 1
  })
  
  // bar 转化为响应式对象
  const state = toRef(obj, 'bar')
  
  const change = () => {
    state.value++
    console.log(obj, state);
  }
  ```
  </div>

  <div class="flex-grow mx-2">

  **toRefs**

  ```js
  import { reactive, toRefs } from 'vue'
  const obj = reactive({
    foo: 1,
    bar: 1
  })
  
  let { foo, bar } = toRefs(obj)
  
  foo.value++
  console.log(foo, bar);
  ```
  </div>
  <div class="flex-grow">
  
  **toRaw**

  ```js
  import { reactive, toRaw } from 'vue'
 
  const obj = reactive({
    foo: 1,
    bar: 1
  })
  
  // 响应式对象转化为普通对象
  const state = toRaw(obj)
  
  const change = () => {
    console.log(obj, state);
  }
  ```
  </div>
</div>

---

# computed 用法
 
计算属性就是当依赖的属性的值发生变化的时候，才会触发他的更改，如果依赖的值，不发生变化的时候，使用的是缓存中的属性值。

<div class="mt-12 min-h-1 !text-3xl" ></div>
<div class="flex">
  <div class="flex-grow mr-1">

  ```js
  import { computed, reactive, ref } from 'vue'

  let price = ref(0)
  
  let m = computed(()=>{
    return `$` + price.value
  })
  
  price.value = 500
  ```

  </div>
  <div class="flex-grow ml-1">

  ```html
  <template>
    <div>{{ mul }}</div>
    <div @click="mul = 100">click</div>
  </template>
  
  <script setup>
    import { computed, ref } from 'vue'
    let price = ref(1)
    let mul = computed({
      get: () => {
        return price.value
      },
      set: (value) => {
        price.value = 'set' + value
      }
    })
  </script>
  ```

  </div>
</div>
---

# watch 用法
 
侦听一个或多个响应式数据源，并在数据源变化时调用所给的回调函数。

<div class="mt-8 min-h-1 !text-3xl" ></div>
<div class="flex">
  <div class="flex-grow mr-2">

  **侦听一个 ref：**

  ```js
  const count = ref(0)

  watch(count, (count, prevCount) => {
    /* ... */
  }, {
    // 在侦听器创建时立即触发回调。
    immediate：false,
    // 如果源是对象，强制深度遍历，以便在深层级变更时触发回调。
    deep: 默认：false,
    // 侦听器将在组件渲染之前执行 'pre' | 'post' | 'sync'
    flush: 'pre'
  })
  ```

  </div>
  <div class="flex-grow">

  **侦听一个 getter 函数：**

  ```js
  const state = reactive({ count: 0 })
  watch(
    () => state.count,
    (count, prevCount) => {
      /* ... */
    }
  )
  ```

  </div>
</div>

---

# RFC

`<script setup>`语法糖，解决Vue3.0中setup需要频繁将声明的变量、函数以及import引入的内容通过return向外暴露，才能在`<template/>`使用的问题

<style>
  .slidev-layout {
    @apply !text-4xl
  }
</style>
<div class="flex gap-4 w-full mt-6">
  <div class="flex-grow w-1/2">

  ```html
  <script>
  import { reactive } from 'vue'

  export default {
    setup() {
      const state = reactive({ count: 0 })

      function increment() {
        state.count++
      }

      return {
        state,
        increment
      }
    }
  }
  </script>
  ```

  </div>
  <div class="flex-grow w-1/2">

  ```html
  <script setup>
  import { reactive } from 'vue'

  const state = reactive({ count: 0 })

  function increment() {
    state.count++
  }
  </script>

  ```

  </div>
</div>

---

# Vue Demo

<div class="overflow-hidden absolute top-24 left-3 text-center">
  <iframe src="https://sfc.vuejs.org/#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"
    width="960"
    height="460"
    class="-mt-14 mb-2"
></iframe>
<a 
class="text-blue-600 underline"
href="https://sfc.vuejs.org/#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"
>
sfc.vuejs.org</a>
</div>

---

# Slidev 介绍

<div class="flex mt-12">
  <div class="flex-grow text-center">
  
  <img src="/slidev.png" width="350">

  <a class="text-blue-600 text-2xl" href="https://www.sli.dev">www.sli.dev</a>
  
  </div>
  <div class="flex-grow text-2xl">

  <div v-click>

  * 支持 Markdown 语法
  * 可定制主题
  * 对开发者友好
  * 快速（基于vite + vue3 + windi css）
  * Recording im Browser
  * VS Code 插件
  * 导出为 PDF，甚至是可托管的单页应用程序

  </div>

  </div>
</div>
