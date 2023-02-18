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
* 可维护性高

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
    * 只对比带有标记的,减少了非动态内容的对比消耗
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
<img src="/vite-project-2.png" class="h-100 rounded ml-2">
</div>

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

```html{all|9}
<template>
  <div v-memo="[valueA, valueB]">
    <ul>
      <li v-for="it in list">{{it}}</li>
    </ul>
  </div>
  <div>
    <span>{{list}}</span>
    <button @click="add">test</button>
  </div>
</template>
<script setup>
import { ref } from 'vue'

const valueA = ref('A')
const valueB = ref('B')

const list = ref([1, 2, 3, 4, 5])

function add() {
  list.value.push('new')
}
</script>
```

<div v-click class="mt-8 min-h-1 text-2xl font-bold">
Virtual DOM
</div>

<div v-after class="mt-4">

* VNodes sind nun flache Objekte
* geringerer Memory Footprint
* schnelleres Diffing

</div>

---

# Ein Blick auf den Compiler

<div class="overflow-hidden absolute top-24 left-3 text-center">
  <iframe src="https://sfc.vuejs.org/#eyJBcHAudnVlIjoiPHRlbXBsYXRlPlxuICA8aDE+V2VsY29tZSE8L2gxPlxuICA8ZGl2IGNsYXNzPVwic3RhdGljXCI+XG4gICAgPE15Q29tcG9uZW50XG4gICAgICBwcm9wMT1cInN0YXRpY1wiXG4gICAgICA6c3VidGl0bGU9XCJzdWJ0aXRsZVwiXG4gICAgPlxuICAgICAgPHNwYW4+IHt7IG1zZyB9fTwvc3Bhbj5cbiAgICA8L015Q29tcG9uZW50PlxuICA8L2Rpdj5cbjwvdGVtcGxhdGU+XG5cbjxzY3JpcHQ+XG4gIGltcG9ydCB7IHJlZiB9IGZyb20gJ3Z1ZSdcbiAgaW1wb3J0IE15Q29tcG9uZW50IGZyb20gJy4vTXlDb21wb25lbnQudnVlJ1xuICBcbiAgZXhwb3J0IGRlZmF1bHQge1xuICAgIGNvbXBvbmVudHM6IHtcbiAgICAgIE15Q29tcG9uZW50LFxuICAgIH0sXG4gICAgc2V0dXAoKSB7XG5cdFx0XHRjb25zdCBtc2cgPSAnSGVsbG8gV29ybGQhJ1xuXHRcdFx0Y29uc3Qgc3VidGl0bGUgPSByZWYoJ1RoaXMgaXMgdGhlIHN1YnRpdGxlJylcbiAgICAgIHJldHVybiB7XG4gICAgICAgIG1zZywgc3VidGl0bGVcbiAgICAgIH1cbiAgICB9XG4gIH1cbjwvc2NyaXB0PiIsIk15Q29tcG9uZW50LnZ1ZSI6Ijx0ZW1wbGF0ZT5cbiAgPHNsb3QgLz5cbjwvdGVtcGxhdGU+XG48c2NyaXB0PlxuZXhwb3J0IGRlZmF1bHQge1xuICBwcm9wczogWydwcm9wMScsICdzdWJ0aXRsZSddXG59XG48L3NjcmlwdD4ifQ=="
    width="960"
    height="460"
    class="-mt-14 mb-2"
></iframe>
<a 
class="text-blue-600 underline"
href="https://sfc.vuejs.org/#eyJBcHAudnVlIjoiPHRlbXBsYXRlPlxuICA8aDE+V2VsY29tZSE8L2gxPlxuICA8ZGl2IGNsYXNzPVwic3RhdGljXCI+XG4gICAgPE15Q29tcG9uZW50XG4gICAgICBwcm9wMT1cInN0YXRpY1wiXG4gICAgICA6c3VidGl0bGU9XCJzdWJ0aXRsZVwiXG4gICAgPlxuICAgICAgPHNwYW4+IHt7IG1zZyB9fTwvc3Bhbj5cbiAgICA8L015Q29tcG9uZW50PlxuICA8L2Rpdj5cbjwvdGVtcGxhdGU+XG5cbjxzY3JpcHQ+XG4gIGltcG9ydCB7IHJlZiB9IGZyb20gJ3Z1ZSdcbiAgaW1wb3J0IE15Q29tcG9uZW50IGZyb20gJy4vTXlDb21wb25lbnQudnVlJ1xuICBcbiAgZXhwb3J0IGRlZmF1bHQge1xuICAgIGNvbXBvbmVudHM6IHtcbiAgICAgIE15Q29tcG9uZW50LFxuICAgIH0sXG4gICAgc2V0dXAoKSB7XG5cdFx0XHRjb25zdCBtc2cgPSAnSGVsbG8gV29ybGQhJ1xuXHRcdFx0Y29uc3Qgc3VidGl0bGUgPSByZWYoJ1RoaXMgaXMgdGhlIHN1YnRpdGxlJylcbiAgICAgIHJldHVybiB7XG4gICAgICAgIG1zZywgc3VidGl0bGVcbiAgICAgIH1cbiAgICB9XG4gIH1cbjwvc2NyaXB0PiIsIk15Q29tcG9uZW50LnZ1ZSI6Ijx0ZW1wbGF0ZT5cbiAgPHNsb3QgLz5cbjwvdGVtcGxhdGU+XG48c2NyaXB0PlxuZXhwb3J0IGRlZmF1bHQge1xuICBwcm9wczogWydwcm9wMScsICdzdWJ0aXRsZSddXG59XG48L3NjcmlwdD4ifQ=="
>
sfc.vuejs.org</a>
</div>

---

# Wo steht das Vue Framework?
Offizielle Libraries

<div class="mt-4 min-h-1"></div>

<div class="flex">
  <div class="flex-grow">

  **Stable**

  * Vue 3.0 (_18.09.2020_)
  * Vue CLI (Vue 3 Support) (_18.09.2020_)
  * eslint-plugin-vue 7.0 (_30.09.2020_)
  * vue-loader 16.0 (_25.11.2020_)
  * Vue Router 4.0 (_07.12.2020_)
  * Vuex 4.0 (_02.02.2021_)

  </div>

  <div v-click class="flex-grow">

  **Release Candidate**
  * @vue/test-utils - 2.0.0-rc.6
  
  </div>

  <div v-click class="flex-grow">

  **Beta**

  * vue-devtools 6.0.0-beta.11
  * rollup-plugin-vue: 6.0.0-beta.11
  </div>

</div>

<hr v-click class="border-t-2 border-vgreen w-xl mt-8">
<div v-after class="mt-4">

* Offizielles Ökosystem fast vollständig stable
* Q1/Q2 2021 wichtige Stablisierungsphase
* Vue 3 bekam 11 Patch releases und erstes Minor Release 3.1 (07.06.2021)

</div>

---

# Community Ökosystem

<div class="mt-12 min-h-1"></div>

<div class="flex">
  <div class="flex-grow">
  
  **Frameworks**

  * Ant Design Vue - <Badge type="success">stable</Badge>
  * Element-Plus - <Badge type="success">stable</Badge>
  * Quasar - <Badge type="warn">Beta</Badge>
  * Vuetify - <Badge type="warn">Alpha</Badge>
  * Nuxt - <Badge type="info">First beta announced</Badge>
  * ChakraUI/Vue <Badge>under development</Badge>

  </div>

  <div class="flex-grow">

  **Integrationen**

  * VSCode (Volar)
  * Jetbrains Webstorm / PHPStorm etc
  * Storybook <code>v6.3</code>
  * Cypress
  * Vite

  </div>
</div>

---

# Next -> Latest
 
<div class="mt-12 min-h-1 !text-3xl" ></div>

Bisher:

```bash
npm i vue@next
```

Ab Q3-2021:

```bash
npm i vue
```


---

# Vue 3 Contributions

<div class="flex mt-12 gap-12">
  <div class="w-1/2 text-center">
  
  <h2>Vue 2</h2>
  <span class="italic text-sm">seit 11.06.2016</span>

  <span class="text-4xl font-bold">1.036</span><br> merged PRs
  <hr class="w-9/12 my-8">
  <span class="text-4xl font-bold">399</span><br> Contributors

  
  </div>
  <div v-click class="w-1/2 text-center">

  <h2>Vue 3</h2>
  <span class="italic text-sm">seit 03.01.2020</span>

  <span class="text-4xl font-bold">1.372</span><br> merged PRs
  <hr class="w-9/12 my-8">
  <span class="text-4xl font-bold">234</span><br> Contributors
  
  </div>
</div>

<hr v-click class="mt-8 mb-12">

<h2 v-after class="text-center">
  PS: Vue 2 wurde gerade 5 Jahre alt! 🥳
</h2>

---
layout: section
---

# Ein "kleines" Major Release
Für Developer

---

# Was hat sich _genau_ geändert?

<div class="mt-12 min-h-1"></div>

* Es gibt 33 Einträge im Migration Guide
* davon sind 3 aber neue Funktionen (Fragments, Suspense)
* Die meisten "Breaking Changes" sind "one-liner" Fixes.


<div class="mt-8 min-h-1"></div>
<span v-click class="text-2xl">Was bedeutet das für Developer?</span>

<div v-click class="mt-4">

* Die Migration (fast) jedes Breaking Change ist *einfach*
* Aber die Migration _aller_ Changes ist *zeitaufwändig*

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

<hr class="mt-4 mb-8">

* Einmalige Änderungen
* Verbesserung: Mehrere Apps auf einer Seite sind besser isoliert.

---

# Lifecycle Hooks

<div class="flex justify-between">
  <div class="flex-grow mr-2">

```html{all|9}
<template>
  <h1>{{ message }}</h1>
</template>
<script>
export default {
  data: () => ({
    message
  }),
  beforeDestroy() {
    console.log('Destruction imminent!')
  }
}
</script>
```

  </div>
  <div class="flex-grow">

```html{all|9}
<template>
  <h1>{{ message }}</h1>
</template>
<script>
export default {
  data: () => ({
    message
  }),
  beforeUnmount() {
    console.log('Destruction imminent!')
  }
}
</script>
```

  </div>
</div>

---
layout: section
---

# `@vue/compat`
## Migration mit der Compat Build (Vue 3.1)

---
layout: big-bullets
heading: Warum eine Migration Build?
title: Warum eine Migration Build?
---

* Migration großer Projekte nicht "an einem Wochenende"
* Dependencies sind noch nicht alle Vue 3 kompatibel
* Deprecation Warnings zeigen notwendige Änderungen auf.

---
layout: big-bullets
heading: Workflow - Initiale Upgrades
title: Workflow - Initiale Upgrades
---

1. Upgrade der notwendigen Dependencies
2. Compat Mode aktivieren
3. App starten
4. Compiler Warnings fixen (z.B. wegen Filters)
5. Auf Vuex `4.0` upgraden
6. Auf VueRouter `3.0` upgraden

Eure App läuft jetzt auf Vue 3 - mit Vue 2 Component Syntax! <span class="text-2xl">🤯</span>

---
layout: big-bullets
heading: Workflows für die Migration
title: Workflows für die Migration
---

<div class="mb-12 text-3xl text-center">2 Varianten:</div>

1. Migration per Feature
2. Migration per Component

---
layout: default
---

# Migration - per Feature

<div class="flex mt-8">

<div v-click class="flex-grow w-1/2 pr-2">

* Ein Feature aussuchen - z.B. Lifecycle hooks
* in jeder Component migrieren

Von Vue 2:

```js{2}
export default {
  beforeDestroy() {
    this.doSomething()
  }
}
```

zu Vue 3:

```js{2}
export default {
  beforeUnmount() {
    this.doSomething()
  }
}
```

</div>
<div v-click class="flex-grow w-1/2 border-l border-vgreen pl-2">

* Anschließend das compat feature global deaktivieren

```js{8-10}
// main.js
import { 
createApp,
configureCompat 
} from 'vue'
import App from './App.vue'

configureCompat({
  OPTIONS_BEFORE_DESTROY: false,
})

createApp(App).mount('#app')
```

</div>

</div>

---

# Migration - per Component

* Alle Migrationen in einer Component vornehmen

<div class="flex mt-8">

<div v-click class="flex-grow w-1/2 pr-2">

```js{2,4,8,11}
export default {
  props: ['value']
  components: {
    Child: () => import('./Child.vue')
  },
  methods: {
    update(value) {
      this.$emit('input', value)
    },
  },
  beforeDestroy() {
    this.doSomething()
  }
}
```

</div>
<div v-click class="flex-grow w-1/2 border-l border-vgreen pl-2">

```js{2-5,7-9,13,16}
export default {
  compatConfig: {
    MODE: 3,
  },
  props: ['modelValue']
  components: {
    Child: defineAsyncComponent(
      () => import('./Child.vue')
    )
  },
  methods: {
    update(value) {
      this.$emit('update:modelValue', value)
    },
  },
  beforeUnmount() {
    this.doSomething()
  }
}
```

</div>

</div>


---
layout: big-bullets
heading: Tips
title: Tips
--- 

* Ihr werdet eine **MENGE** Warnings sehen - keine Panik!
  * Nur in development
  * Minimaler Perf-Overhead, wettgemacht durch Vue 3 Perf-Verbesserungen
* Migriert zuerst "find&replace" features global in allen Components
* Migriert danach einzelne Components
* Migriert zuletzt eure dependencies auf ihre Vue 3 versionen

---

# Migration Build docs

<iframe
class="w-full h-9/10 mx-auto"
src="https://v3.vuejs.org/guide/migration/migration-build.html"
></iframe>

---
layout: section
---

# Mehr als ein Major Release
## Wohin die Reise geht

---
layout: big-bullets
heading: DX - IDE Integration
title: DX - IDE Integration
---

* Derzeit 3 Extensions: Vetur, VueDX, Volar
* Neues Fundament wird Volar sein
* Language Server Implementation auch für andere IDEs
* **Type Hints / Autocomplete in Templates!**

<div v-click class="absolute bottom-8 w-full">
  <img src="/volar.png" class="w-6/10">
</div>


---
layout: big-bullets
heading: DX - Devtools 6.0
title: DX - Devtools 6.0
---

* Neu: Performance Messung
* Neu: Events timeline
* Neu: Plugin API

---

# Performance Messung

<img class="mx-auto" src="/devtools-perf1.png">
<img class="mx-auto mt-12" src="/devtools-perf2.png">

---

# Plugin API

<img class="mx-auto" src="/pinia.png">
<br>
<div class="text-center">
  <a class="text-xl text-blue-600" href="https://devtools.vuejs.org/plugin/plugins-guide.html">Plugin API Docs</a>
</div>

---

# RFCs - `<script setup>`

<style>
  .slidev-layout {
    @apply !text-4xl
  }
</style>
<div class="flex gap-4 w-full mt-12">
  <div class="flex-grow w-1/3">

  * Reduziert boilerplate
  * Performance-Potentiale

  <div class="mt-12">
    <a class="text-xl text-blue-600" href="https://github.com/vuejs/rfcs/pull/227">Link zum RFC</a>
  </div>

  </div>
  <div class="flex-grow w-2/3">

  ```html
  <script setup>
  import Foo from './Foo.vue'
  import { ref, defineProps } from 'vue'

  const props = defineProps({
    title: String,
  })

  const count = ref(0)
  const inc = () => { count.value++ }
  </script>

  <template>
    <h1>{{ props.title }}</h1>
    <Foo :count="count" @click="inc" />
  </template>
  ```

  </div>
</div>


---

# Dieser Talk wurde mit Slidev gebaut

<div class="flex mt-12">
  <div class="flex-grow text-center">
  
  <img src="/slidev.png" width="350">

  <a class="text-blue-600 text-2xl" href="https://www.sli.dev">www.sli.dev</a>
  
  </div>
  <div class="flex-grow text-2xl">

  <v-clicks>

  * Vite
  * Slides mit Markdown schreiben
  * Vue 3 Components in Markdown
  * Presenter Mode
  * Recording im Browser
  * VS Code Extension
  * PDF Export
  * Deployable als App

  </v-clicks>

  <a v-click class="text-blue-600 text-2xl" href="https://vueday-2021.linusb.org">vueday-2021.linusb.org</a>

  
  </div>
</div>
