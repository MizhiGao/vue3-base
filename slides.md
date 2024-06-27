---
# You can also start simply with 'default'
theme: default
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
background: https://cover.sli.dev
# some information about your slides (markdown enabled)
title: Vue3基础
info: |
  ##
  Learn more at [vuejs](https://cn.vuejs.org/)
# apply unocss classes to the current slide
class: text-center
# https://sli.dev/custom/highlighters.html
highlighter: shiki


# 幻灯片的配色方案，可以使用 'auto'，'light' 或者 'dark'
colorSchema: auto
# https://sli.dev/guide/drawing
drawings:
  persist: false
# slide transition: https://sli.dev/guide/animations#slide-transitions
transition: slide-left
# enable MDC Syntax: https://sli.dev/guide/syntax#mdc-syntax
mdc: true
---

# Vue3基础

<div class="pt-12">
  <span @click="$slidev.nav.next" class="px-2 py-1 rounded cursor-pointer" hover="bg-white bg-opacity-10">
    高咪咪 <carbon:arrow-right class="inline"/>
  </span>
</div>

<div class="abs-br m-6 flex gap-2">
  <button @click="$slidev.nav.openInEditor()" title="Open in Editor" class="text-xl slidev-icon-btn opacity-50 !border-none !hover:text-white">
    <carbon:edit />
  </button>
  <a href="https://github.com/slidevjs/slidev" target="_blank" alt="GitHub" title="Open in GitHub"
    class="text-xl slidev-icon-btn opacity-50 !border-none !hover:text-white">
    <carbon-logo-github />
  </a>
</div>

---
transition: fade-out
---

# 什么是Vue?

Vue (发音为 /vjuː/，类似 view) 是一款用于构建用户界面的 JavaScript 框架。它基于标准 HTML、CSS 和 JavaScript 构建，并提供了一套声明式的、组件化的编程模型，帮助你高效地开发用户界面。

Vue 3 的新特性
- **组合式API** - 这是Vue 3最重要的新特性之一，它允许更灵活、更逻辑化地组织代码。
- **更好的性能** - Vue 3的虚拟DOM重写，提供了更快的挂载、修补和渲染速度。
- **更小的打包大小** - 由于新的架构和树摇技术，Vue 3的打包大小比Vue 2小。
- **更好的TypeScript支持** - Vue 3在内部使用了TypeScript，因此它为开发者提供了更好的TypeScript支持。

---
layout: default
layoutClass: gap-4
---

# 什么是组合式API？

在 Vue 3 中引入的一种新的编写 Vue 组件的方式。

````md magic-move {lines: true}
```js {all|5|9-11|13-15|all}
<script>
export default {
  data() {
    return {
      count: 0
    }
  },
  methods: {
    increment() {
      this.count++
    }
  },
  mounted() {
    console.log(`The initial count is ${this.count}.`)
  }
}
</script>
<template>
  <button @click="increment">Count is: {{ count }}</button>
</template>
```


```vue
<script>
import { ref, onMounted } from 'vue'
export default{
  setup(){ //setup 函数是组件的入口点，在组件实例被创建和初始化之后，但在渲染发生之前被调用。
    // 响应式状态
    const count = ref(0)
    // 用来修改状态、触发更新的函数
    function increment() {
      count.value++
    }
    // 生命周期钩子
    onMounted(() => {
      console.log(`The initial count is ${count.value}.`)
    })
    return{
      count,
      increment
    }
  }
}
</script>

<template>
  <button @click="increment">Count is: {{ count }}</button>
</template>
```



```vue
<script setup>
import { ref, onMounted } from 'vue'

// 响应式状态
const count = ref(0)

// 用来修改状态、触发更新的函数
function increment() {
  count.value++
}

// 生命周期钩子
onMounted(() => {
  console.log(`The initial count is ${count.value}.`)
})
</script>

<template>
  <button @click="increment">Count is: {{ count }}</button>
</template>
```
````

---
transition: fade-out
---

# `<script setup>` 语法糖
- setup 函数

setup() 函数是 vue3 中，专门为组件提供的新属性。它为我们使用 vue3的 Composition API 新特性提供了统一的入口, setup 函数会在 beforeCreate 、created 之前执行, vue3也是取消了这两个钩子，统一用setup代替, 该函数相当于一个生命周期函数，vue中过去的data，methods，watch等全部都用对应的新增api写在setup()函数中

setup() 接收两个参数 props 和 context。它里面不能使用 this，而是通过 context 对象来代替当前执行上下文绑定的对象，context 对象有四个属性：attrs、slots、emit、expose

里面通过 ref 和 reactive 代替以前的 data 语法，return 出去的内容，可以在模板直接使用，包括变量和方法

- script setup 语法糖

script setup是在单文件组件 (SFC) 中使用组合式 API 的编译时语法糖。相比于普通的 script 语法更加简洁

要使用这个语法，需要将 setup attribute 添加到 `<script>` 代码块上：

这种写法会自动将所有顶级变量、函数，均会自动暴露给模板（template）使用
这里强调一句 “暴露给模板，跟暴露给外部 (defineExpose) 不是一回事”

**调用时机**

创建组件实例，然后初始化 props ，紧接着就调用setup 函数。从生命周期钩子的视角来看，它会在 beforeCreate 钩子之前被调用.
<style>
p{
  font-size: 12px;
  margin-top: 0.25rem;
  margin-bottom: 0.25rem;
}
</style>
---
transition: slide-up
level: 2
---

## 创建一个Vue 3 项目
使用`create-vue`创建项目
前提环境条件：已安装Node.js
```shell
npm init vue@latest
```
<div grid="~ cols-2 gap-1">
<div>
  我们按照提示需求进行安装即可
 <img v-click class="h-300px" src="/install.png" />
</div>

<v-click>

```js
/** src/main.js */
/** 1. 引入必要的模块和组件 */
import './assets/main.css' // 引入全局样式文件
import { createApp } from 'vue'// 创建Vue应用的基础
import App from './App.vue'  // 引入根组件
import { createPinia } from 'pinia' // 导入了 createPinia 函数
import router from './router' // 导入了 router 实例

/** 2. 创建Vue应用实例 */
const app = createApp(App)

/** 3. 注册插件和路由 方便全局使用 */
// 将Pinia注册到Vue应用中，用于管理应用的状态。
app.use(createPinia())
// 将Vue Router注册到Vue应用中，用于管理页面路由。
app.use(router)

/**4. 挂载Vue应用 */
// 将Vue应用挂载到DOM中的#app元素上
app.mount('#app')

```
</v-click>
</div>


<style>
  .slidev-code{
    font-size:12px
  }
</style>

---
layout: cover
class: text-center
---

# ref vs reactive

Vue 3提供了两个主要的函数来创建响应式数据：ref 和 reactive。

但这两者有什么区别，什么情况下用 ref，什么情况下用 reactive 呢？

---

# ref
接受一个内部值，返回一个响应式的、可更改的 ref 对象，此对象只有一个指向其内部值的属性 .value。
- 参数

ref 的参数可以是：基本数据类型、引用数据类型、DOM的ref属性值

- 使用

在模板中使用 ref 时，我们不需要加 `.value`，因为当 ref 在模板中作为顶层属性被访问时，它们会被自动解包，但在js中，访问和更新数据都需要加 `.value`。

```ts {all|3-4,6-7,12-13}
<script setup>
  import { ref } from 'vue'
  const product = ref({ price: 0 })
  const total = ref(100)
  const changeProductPrice = () => {
    product.value.price += 10
    total.value += 10
  }
</script>
<template>
  <div class="main">
    <p>price: {{ product.price }}</p>
    <p>total: {{ total }}</p>
    <button @click="changeProductPrice">修改产品价格</button>
  </div>
</template>
```

<style>
ul,li{
  font-size: 12px
}

p{
  font-size: 0.75rem;
  margin-top: 0.25rem;
  margin-bottom: 0.25rem;
}
</style>

---

# reactive

- 作用:

reactive 的作用是将一个普通的对象转换成响应式对象。它会递归地将对象的所有属性转换为响应式数据。它返回的是一个 Proxy 对象。

- 参数

reactive 的参数只能是对象或者数组或者像 Map、Set 这样的集合类型。

- 基本用法
```vue
<script setup>
  import { reactive } from 'vue'

  // 使用 reactive 创建一个包含多个响应式属性的对象
  const person = reactive({
    name: 'Echo',
    age: 25,
  })

  console.log(person.name); // 读取属性值：'Echo'
  person.age = 28;          // 修改属性值
  console.log(person.age);  // 读取修改后的属性值：28

</script>
```

<style>
ul,li{
  font-size: 12px
}

p{
  font-size: 0.75rem;
  margin-top: 0.25rem;
  margin-bottom: 0.25rem;
}
</style>

---

# reactive 局限性：

- 响应性丢失：
```javascript
const state = reactive({ count: 0 });

// 函数接收的是普通数字，无法跟踪 state.count 的变化
callSomeFunction(state.count);

// 解构导致响应性丢失
let { count } = state;
count++;

// 无法替换整个对象
let state = reactive({ count: 0 });
// 创建了一个新的响应式对象并将其分配给 state 变量
// 只是改变了 state 变量的引用，不会影响原来的响应式对象
state = reactive({ count: 1 });  // 不会生效
```

在组合式 API 中，推荐使用 ref() 函数来声明响应式状态

---
transition: slide-up
---

# 模板语法
Vue 使用一种基于 HTML 的模板语法，使我们能够声明式地将其组件实例的数据绑定到呈现的 DOM 上。

<div grid="~ cols-2 gap-2">
<div>文本插值</div>
<div>原始 HTML</div>
```vue
<span>Message: {{ msg }}</span>
const msg = ref('Hello World')
```

```vue
const rawHtml = ref('<span style="color:red">Hi!</span>')
<template>
  <p>Using v-html directive:
    <span v-html="rawHtml"></span>
</p>
</template>
```
<!-- ./components/HelloWorld.vue -->
<HelloWorld v-click />

<HtmlRender v-click />

</div>

- 文本插值

最基本的数据绑定形式是文本插值，它使用的是“Mustache”语法 (即双大括号)：双大括号标签会被替换为相应组件实例中 msg 属性的值。同时每次 msg 属性更改时它也会同步更新。

- 原始 HTML

双大括号会将数据解释为纯文本，而不是 HTML。若想插入 HTML，你需要使用 v-html 指令：


---

# 模板语法

- Attribute 绑定

双大括号不能在 HTML attributes 中使用。想要响应式地绑定一个 attribute，应该使用 v-bind 指令：
````md magic-move
```vue
<div v-bind:id="dynamicId"></div>
```

```vue
<div :id="dynamicId"></div>
```

```vue
<div :id="id"></div>
```

```vue
<div :id></div>
```
````

- 动态绑定多个值
````md magic-move
```vue
const objectOfAttrs = {
  id: 'container',
  class: 'wrapper'
}

<div v-bind="objectOfAttrs"></div>
```

```vue
const objectOfAttrs = {
  id: 'container',
  class: 'wrapper'
}

<div :id="objectOfAttrs.id" :class="objectOfAttrs.class"></div>
```
````

- 使用 JavaScript 表达式

```js
{{ number + 1 }}

{{ ok ? 'YES' : 'NO' }}

{{ message.split('').reverse().join('') }}

```
---
layout: two-cols
layoutClass: gap-4
transition: fade-out
---

# computed

````md magic-move {lines:true}
```vue
<script setup>
import { reactive, computed } from 'vue'

const arr = ref([1,2,3,4,5,6,7])
</script>

<template>
  <p>原始数组:{{ arr }}</p>
  <span>
    {{ arr.value.filter((item) => item > 2) }}
  </span>
</template>
```

```ts
<script setup>
import { reactive, computed } from 'vue'

const arr = ref([1,2,3,4,5,6,7])

// 一个计算属性 ref
const arrFilter = computed(() => {
  return arr.value.filter((item) => item > 2)
})
</script>

<template>
  <p>原始数组:{{ arr }}</p>
  <span>{{ arrFilter }}</span>
</template>
```
````
::right::

计算属性（computed properties）是基于响应式依赖进行缓存的属性。它们只有在其依赖发生变化时才会重新计算。这使得计算属性非常适合处理复杂逻辑和性能优化。

- 注意点

**计算属性中不应该有"副作用"**

比如: 异步请求/修改dom

什么副作用,计算属性的主要作用是依赖响应式数据进行计算获取一个新的值,除了这个作用之外,我们加上去别的都是副作用

这些副作用,我们可以交给watch来做

**避免直接修改计算属性的值**

从计算属性返回的值是派生状态。可以把它看作是一个“临时快照”，每当源状态发生变化时，就会创建一个新的快照。
更改快照是没有意义的，因此计算属性的返回值应该被视为只读的，并且永远不应该被更改——应该更新它所依赖的源状态以触发新的计算。

<style>
p {
  font-size:14px
}
</style>

---
layout: two-cols
layoutClass: gap-2
---

# 类与样式绑定

- 绑定 HTML class

```vue
<!-- /绑定对象/ -->
<div :class="{ active: isActive }"></div>
<!-- :class 指令也可以和一般的 class attribute 共存 -->
<div class="static" :class="{ active: isActive, 'text-danger': hasError }"></div>

const classObject = reactive({
  active: true,
  'text-danger': false
})

<div :class="classObject"></div>
```

```vue
<!-- 绑定数组 -->
const activeClass = ref('active')
const errorClass = ref('text-danger')
<div :class="[activeClass, errorClass]"></div>
<div :class="[isActive ? activeClass : '', errorClass]"></div>
```


::right::

绑定内联样式

``` vue
<!-- 绑定对象 -->
<!-- :style 支持绑定 JavaScript 对象值，对应的是 HTML 元素的 style 属性： -->
const activeColor = ref('red')
const fontSize = ref(30)

<div :style="{ color: activeColor, fontSize: fontSize + 'px' }"></div>

const styleObject = reactive({
  color: 'red',
  fontSize: '30px'
})
<div :style="styleObject"></div>
```

```vue {all|13}{maxHeight:'100'}
<!-- 绑定数组 -->
<!-- :style 绑定一个包含多个样式对象的数组。这些对象会被合并后渲染到同一元素上 -->
const styleArray = reactive([
  {
    color: 'blue', // 样式对象1
    fontSize: '14px'
  },
  {
    backgroundColor: 'yellow', // 样式对象2
    padding: '10px'
  }
])
<div :style="styleArray"></div>
```

---
layout: two-cols
layoutClass: gap-2
---

# 条件渲染

<ConditionalRendering />

```js
<div v-if="type == 'A'">A</div>
<div v-else-if="type == 'B'">B</div>
<div v-else-if="type == 'C'">C</div>
<div v-else>Not A/B/C</div>
```

`v-if`

- 是“真实的”按条件渲染，因为它确保了在切换时，条件区块内的事件监听器和子组件都会被销毁与重建。
- 是惰性的：如果在初次渲染时条件值为 false，则不会做任何事。条件区块只有当条件首次变为 true 时才被渲染。
- 有更高的切换开销

::right::

```js {13-14}
<script setup>
import { ref } from 'vue'

const awesome = ref(true)

function toggle() {
  awesome.value = !awesome.value
}
</script>

<template>
  <button @click="toggle">toggle</button>
  <h1 v-if="awesome">Vue is awesome!</h1>
  <h1 v-else>Oh no 😢</h1>
</template>
```

`v-show`

- 会在 DOM 渲染中保留该元素；
- 仅切换了该元素上名为 `display` 的CSS属性。
- 不支持在 `<template>` 元素上使用，也不能和 `v-else` 搭配使用。
- 有更高的初始渲染开销

<style>
ul,li{
  font-size:14px
}
</style>

---

# 列表渲染
`v-for`
<div grid="~ cols-2 gap-2">

```vue
const parentMessage = ref('Parent')
const items = ref([{ message: 'Foo' }, { message: 'Bar' }])

<li v-for="(item, index) in items">
  {{ parentMessage }} - {{ index }} - {{ item.message }}
</li>
```

```vue
const myObject = ref({
  title: 'How to do lists in Vue',
  author: 'Jane Doe',
  publishedAt: '2016-04-10'
})
<li v-for="(value, key) in myObject">
  {{ key }}: {{ value }}
</li>
```

</div>


你也可以使用 `v-for` 来遍历一个对象的所有属性。遍历的顺序会基于对该对象调用 `Object.keys()` 的返回值来决定。



**同时使用 v-if 和 v-for 是不推荐的**

当它们同时存在于一个节点上时，`v-if` 比` v-for` 的优先级更高。这意味着 `v-if` 的条件将无法访问到 `v-for` 作用域内定义的变量别名。

<style>
p {
  font-size:12px
}
</style>

---

# 事件处理

### 监听事件
我们可以使用 v-on 指令 (简写为 @) 来监听 DOM 事件，并在事件触发时执行对应的 JavaScript。

用法：`v-on:click="handler"` 或 `@click="handler"`。
事件处理器 (handler) 的值可以是：

内联事件处理器：事件被触发时执行的内联 JavaScript 语句 (与 onclick 类似)。
```js
const count = ref(0)
<button @click="count++">Add 1</button>
<p>Count is: {{ count }}</p>
```

方法事件处理器：一个指向组件上定义的方法的属性名或是路径。

```js {all|12}{maxHeight:'200'}
const name = ref('Vue.js')

function greet(event) {
  alert(`Hello ${name.value}!`)
  // `event` 是 DOM 原生事件
  if (event) {
    alert(event.target.tagName)
  }
}

<!-- `greet` 是上面定义过的方法名 -->
<button @click="greet">Greet</button>
```

<style>
p{
  font-size:14px
}
</style>

---

# 事件修饰符
- `.stop`: 阻止单击事件继续冒泡
  ```html
  <div @click="onStop(1)">
    <div @click="onStop(2)">
      <div @click.stop="onStop(3)">.stop</div>
    </div>
  </div>
  ```
  上面代码如果没加.stop，就会从内至外冒泡，依次执行：onStop(3)、onStop(2)、onStop(1)

  但是我们在onStop(3)的地方加上.stop，点击onStop(3)的时候就只会执行onStop(3),不会向外冒泡了

- `.prevent`: 阻止浏览器的默认行为
    - 超链接的自动跳转
    - form标签中submit 按钮点击导致的页面刷新
    - 网页鼠标右键
- `.capture`: 添加事件侦听器时使用事件捕获模式
- `.self`:  只执行直接作用在该元素身上的事件，会忽略其他元素的冒泡或者捕获
- `.once`: 事件只会触发一次
- `.passive`: 告诉浏览器不用去查询，我们没有preventDefault阻止默认行为

<style>
p,li{
  font-size:12px;
  margin: 0.25rem 0;

}
</style>

---

# 按键修饰符
常用按键别名如下：

- `.enter`: 回车
- `.tab`: 换行(特殊键, 必须配合keydown 去使用)
- `.delete`: 捕获“删除”和“退格”键
- `.esc`: 退回
- `.space`: 空格
- `.up`: 上
- `.down`: 下
- `.left`: 左
- `.right`: 右

```html
<input @keydown.tab="submit" />
<input @keyup.enter="submit" />
```

---

# 系统修饰符
可以用如下修饰符来实现仅在按下相应按键时才触发鼠标或键盘事件的监听器。

- `.ctrl`
- `.alt`
- `.shift`
- `.meta`
```html

<!-- Alt + Enter -->
<input @keyup.alt.enter="clear" />

<!-- Ctrl + Click -->
<div @click.ctrl="doSomething">Do something</div>

<!-- 即使 Alt 或 Shift 被一同按下时也会触发 -->
<button @click.ctrl="onClick">A</button>

<!-- 有且只有 Ctrl 被按下的时候才触发 -->
<button @click.ctrl.exact="onCtrlClick">A</button>

<!-- 没有任何系统修饰符被按下的时候才触发 -->
<button @click.exact="onClick">A</button>
```

---

# 鼠标按钮修饰符

- `.left`
- `.right`
- `.middle`

```js
<div @click.right.prevent="submit">禁止鼠标右键默认事件</div>
```

<style>
p{
  font-size:14px
}
</style>

---
layout: two-cols
---

# 表单输入绑定

<FormBindings/>
<br>
<br>
通过一起使用 v-bind 和 v-on，我们可以为表单输入元素创建双向绑定：

```js
<input
  :value="text"
  @input="event => text = event.target.value">
```
v-model 指令帮我们简化了这一步骤：

```js
<input v-model="text">
```

::right::

#


```js
<script setup>
import { ref } from 'vue'

const text = ref('')
</script>

<template>
  <input v-model="text" placeholder="Type here">
  <p>{{ text }}</p>
</template>
```

另外，v-model 还可以用于各种不同类型的输入，它会根据所使用的元素自动使用对应的 DOM 属性和事件组合：

文本类型的 `<input>` 和 `<textarea>` 元素会绑定 **value property** 并侦听 **input** 事件；

`<input type="checkbox">` 和 `<input type="radio">` 会绑定 **checked property** 并侦听 **change** 事件；

`<select>` 会绑定 **value property** 并侦听 **change** 事件。

---

# 侦听器
在Vue3中可以通过watch或者是watchEffect来创建侦听器。watch需要手动指定监听属性。而watchEffect类型计算属性，它会追踪在回调中使用的属性进行监听。

- watch

作用: 侦听一个或者多个数据的变化,数据变化时执行回调函数

watch接收三个参数:

1 - 需要监听的对象

2 - 侦听器回调函数

3 -  配置对象。

watch 的第一个参数可以是不同形式的“数据源”：它可以是一个 ref (包括计算属性)、一个响应式对象、一个 getter 函数、或多个数据源组成的数组：

- 配置对象

deep: 强制转成深层侦听器

immediate: 强制侦听器的回调立即执行

once: 回调只在源变化时触发一次
<style>
  p{
    font-size:14px;
    margin-top:0.25rem;
    margin-bottom:0.25rem
  }
</style>
---

```ts {monaco-run}
import { ref, watch } from 'vue'
const x = ref(0)
const y = ref(0)

// 单个 ref
watch(x, (newX) => {
  console.log(`x is ${newX}`)
})

x.value = 1

// getter 函数
watch(
  () => x.value + y.value,
  (sum) => {
    console.log(`sum of x + y is: ${sum}`)
  }
)

// 多个来源组成的数组
watch([x, () => y.value], ([newX, newY]) => {
  console.log(`x is ${newX} and y is ${newY}`)
})
```

---

#


1. 使用 watch 侦听 ref 定义的响应式数据（参数是原始数据类型的情况）

```ts {monaco-run}
import { ref, watch } from 'vue'

let count = ref(0)
watch(count, (newValue, oldValue) => {
  console.log(`count的值变化了, 新值:${newValue}，旧值：${oldValue}`)
})
const changeCount = () => {
  count.value += 10;
}
changeCount()
```

---
layout: two-cols
layoutClass: gap-16
transition: fade-out
level:6
---

#

2. 使用 watch 侦听 ref 定义的响应式数据（参数是引用数据类型的情况）
```js {monaco-run}
  import { ref, watch } from 'vue'

  let count = ref({ num: 0 })
  watch(count, () => {
    console.log(`count的值发生变化了`)
  })
  const changeCount = () => {
    count.value.num += 10;
  }
  changeCount()
```
这种情况是因为 watch 并没有对 count 进行深度侦听，但是需要注意的是，此时的 DOM 是能够更新的，

要想深度侦听，只需要加一个对应的参数即可，{ deep: true }。

::right::

```js {monaco-run}
  import { ref, watch } from 'vue'

  let count = ref({ num: 0 })
  watch(count.value, () => {
    console.log(`count的值发生变化了1`)
  })
  // 一个返回响应式对象的 getter 函数
  // 只有在返回不同的对象时，才会触发回调
  // 修改属性值不会触发
  watch(()=>count.value, () => {
    console.log(`count的值发生变化了2`)
  })
  //返回该属性的 getter 函数
  watch(()=>count.value.num, () => {
    console.log(`count的值发生变化了3`)
  })
  const changeCount = () => {
    count.value.num += 10;
  }
  changeCount()
```
---

#

3.  使用 watch 侦听 reactive 定义的响应式数据
```js {monaco-run}
  import { reactive, watch } from 'vue'

  let count = reactive({ nums: {num:0} })
  watch(count, () => {
    console.log(`count的值发生变化了`)
  })
  // 一个返回响应式对象的 getter 函数，只有在返回不同的对象时，才会触发回调
  // 需要添加 deep 属性，才能够对其深度侦听
  watch(()=>count.nums, () => {
    console.log(`count的值发生变化了`)
  },{
    deep: true
  })
  const changeCount = () => {
    count.nums.num += 10;
  }

  changeCount()
```
上面这段代码中,用 watch 函数侦听 reactive 数据时，不需要添加 deep 属性，也能够对其深度侦听。

---
layout: two-cols
layoutClass: gap-2
level: 2
---
# watchEffect()


watch()不设置immediate参数时，仅在侦听数据变化时，才会执行回调。

而watchEffect则会立即执行一次回调，就是说watchEffect会先执行一次回调，然后去追踪在回调中使用过的响应式属性，对这些属性进行追踪监听，当他们发生变化，从新执行回调。


注意1：watchEffect 只有在回调中使用数据才会进行监听。修改属性是不被监听的。（即get属性才会监听，set属性不进行监听）

注意2：watchEffect仅会监听同步使用的属性，在异步中使用属性，不会被追踪监听。

结论：watchEffect只监听同步使用的属性。

注意3：watchEffect是基于属性的追踪，如果监听的属性的值是一个对象，那么修改对象内部的属性，是不被监听到的。（watchEffect不是深度监听）

::right::

#

<div m="t-4"></div>

````md magic-move {lines:true}
```ts
import { watchEffect, ref } from 'vue'
const person = ref({
  age:18,
})
watchEffect(() => {
   let x: number = person.value.age;
   console.log(x,'watchEffect配置的回调执行了')
})

person.value.age = 30;
setTimeout(() => {
   person.value.age = 30;
}, 2000)
```

```ts
watchEffect(() => {
   //在 watchEffect 中修改一个响应式的属性，不被watchEffect追踪监听。
   person.value.age = 20;
   console.log('watchEffect配置的回调执行了')
})
setTimeout(() => {
   person.value.age = 30;//修改了值，但是监听失败。
}, 3000)
```

```ts
watchEffect(() => {
   setTimeout(() => {
      console.log(person.value.age);
   }, 2000)
   console.log('watchEffect配置的回调执行了')
})
setTimeout(() => {
   person.value.age = 30;//修改了值，但是监听失败。
}, 5000)
```

```js
watchEffect(() => {
   //监听property的值是一个对象。
   console.log(person.property);
})

setTimeout(() => {
   person.property.car = true;//修改对象里面的属性，不会被监听到。
}, 3000)

setTimeout(() => {
   //修改property，重新指向一个对象，可以监听到。
   person.property = {
      car: false
   }
}, 5000)
```
````
---

# watch vs. watchEffect​

watch 和 watchEffect 都能响应式地执行有副作用的回调。它们之间的主要区别是追踪响应式依赖的方式：

watch 只追踪明确侦听的数据源。它不会追踪任何在回调中访问到的东西。另外，仅在数据源确实改变时才会触发回调。watch 会避免在发生副作用时追踪依赖，因此，我们能更加精确地控制回调函数的触发时机。

watchEffect，则会在副作用发生期间追踪依赖。它会在同步执行过程中，自动追踪所有能访问到的响应式属性。这更方便，而且代码往往更简洁，但有时其响应性依赖关系会不那么明确。

---
layout: image-right
image: /image-6.png
backgroundSize: contain
level: 2
---

# 生命周期
setup 初始化组件状态，定义响应式数据和方法
- onBeforeMount() 注册一个钩子，在组件被挂载之前被调用。
- onMounted() 注册一个回调函数，在组件挂载完成后执行。
- onBeforeUpdate()注册一个钩子，在组件即将因为响应式状态变更而更新其 DOM 树之前调用。
- onUpdated() 注册一个回调函数，在组件因为响应式状态变更而更新其 DOM 树之后调用。
- onBeforeUnmount()注册一个钩子，在组件实例被卸载之前调用。
- onUnmounted() 注册一个回调函数，在组件实例被卸载之后调用。可以在这个钩子中手动清理一些副作用，例如计时器、DOM 事件监听器或者与服务器的连接。


<style>
li{
  font-size:16px
}
</style>
---

# 组件基础
组件允许我们将 UI 划分为独立的、可重用的部分，并且可以对每个部分进行单独的思考。在实际应用中，组件常常被组织成层层嵌套的树状结构：
![alt text](/image.png)


---
layout: two-cols
layoutClass: gap-2
---

# 定义一个组件

当使用构建步骤时，我们一般会将 Vue 组件定义在一个单独的 .vue 文件中，这被叫做单文件组件 (简称 SFC)：

'./ButtonCounter.vue'
```vue
<script setup>
import { ref } from 'vue'

const count = ref(0)
</script>

<template>
  <button @click="count++">
    You clicked me {{ count }} times.
  </button>
</template>
```

::right::

# 使用组件

通过 `<script setup>`，导入的组件都在模板中直接可用。
要传递动态值，我们还可以使用 v-bind 语法。

<br/>
<br/>

```vue
<script setup>
import ButtonCounter from './ButtonCounter.vue'
<template>
  <h1>Here is a child component!</h1>
  <ButtonCounter />
  <ButtonCounter />
  <ButtonCounter />
</template>

</script>
```

---

#
- 传递props

父组件使用 v-bind 语法 (:title="post.title") 来传递动态 prop 值的

- ​监听事件

父组件可以通过 v-on 或 @ 来选择性地监听子组件上抛的事件，就像监听原生 DOM 事件那样

- `defineProps` 和 `defineEmits`

在 Vue 3 中，defineProps 和 defineEmits 是用于定义组件的 props 和需要抛出的事件方法。

仅可用于 `<script setup>` 之中，并且不需要导入。


`defineEmits` 返回一个等同于 $emit 方法的 emit 函数。

`defineProps` 声明的 props 会自动暴露给模板。

---
layout: two-cols
---

```vue {all|15-18}
<script setup>
import { ref } from 'vue';
import ChildComponent from './ChildComponent.vue';

const message = ref('Hello from Parent Component');

function handleUpdateMessage(newMessage) {
  message.value = newMessage;
}
</script>

<template>
  <div class="body">
    <p>{{ message }}</p>
    <ChildComponent
      :msg="message"
      @updateMessage="handleUpdateMessage"
    />
  </div>
</template>
```


::right::
#
<br>
<ParentComponent1/>

```vue {all|2-8}
<script setup>
const props = defineProps({
  msg: String
});
const emit = defineEmits(['updateMessage']);
function updateMessage() {
  emit('updateMessage', 'Hello from Child Component');
}
</script>
<template>
  <div>
    <p>{{ msg }}</p>
    <button class="button" @click="updateMessage">Send Message to Parent</button>
  </div>
</template>
```

---
layout: center
class: text-center
---

# Thanks！


