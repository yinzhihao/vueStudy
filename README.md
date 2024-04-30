# vueStudy

# 创建项目

需要先切换到node版本为v18.16.0，v12的版本安装报错
nvm use 18.16.0

## 方式一

npm init vue@latest

cd runoob-vue3-test
npm install
npm run format
npm run dev

## 方式二

npm init vite-app runoob-vue3-test2

cd runoob-vue3-test2
cnpm install
cnpm run dev

## 方式三

查看是否安装vue cli
vue -V
安装vue CLI
npm install -g @vue/cli

vue create runoob-vue3-app
cd runoob-vue3-app
npm run serve

疑问❓：为什么目录里少了build、config、static文件夹

## 方式四

界面化
vue ui

# 起步

## 写法一
```javascript
<div id="app" class="demo">
    <input type="text" v-model="message">
    <p>{{ message }}</p>
</div>

<script>
const HelloVueApp = {
  data() {
    return {
      message: 'Hello Vue!!'
    }
  }
}

Vue.createApp(HelloVueApp).mount('#app')
</script>
```

createApp：起点
mount：挂载到DOM元素中

## 写法二
```javascript
const app = Vue.createApp({
  data() {
    return { count: 4 }
  },
  methods: {
    increment() {
      // `this` 指向该组件实例
      this.count++
    }
  }
})

const vm = app.mount('#app')

document.write(vm.count) // => 4
vm.increment()
```

# Vue 指令（Directives）

v-bind    v-bind:src=""
v-if	    v-if=""
v-show	  v-show=""
v-for	    v-for="(item, index) in items" :key="item.id"
v-on	      v-on:click=""
v-model	    v-model=""

# Vue3 模板语法

## 插值

### 文本
{{...}}
v-once 指令执行一次性地插值

### Html
v-html
<span v-html="rawHtml"></span>
rawHtml: '<span style="color: red">这里会显示红色！</span>'

### 属性
v-bind 
<button v-bind:disabled="isButtonDisabled">按钮</button>

绑定class类的样式
<div v-bind:class="{'class1': use}">
  v-bind:class 指令
</div>

### 表达式
{{5+5}}<br>
{{ ok ? 'YES' : 'NO' }}<br>
{{ message.split('').reverse().join('') }}
<div v-bind:id="'list-' + id">菜鸟教程</div>


## 指令
除了前面的，下面补充几个

### 参数
v-bind:属性（src/href）

<!-- 完整语法 -->
v-on:click=""

<!-- 缩写 -->
@click=""

<!-- 动态参数的缩写 (2.6.0+) -->
<a @[event]="doSomething"> ... </a>

### 修饰符
.
<form v-on:submit.prevent="onSubmit"></form>

## 用户输入
v-model：双向绑定，用来在 input、select、textarea、checkbox、radio

## 缩写

### v-bind 缩写
<!-- 完整语法 -->
<a v-bind:href="url"></a>
<!-- 缩写 -->
<a :href="url"></a>

### v-on 缩写
<!-- 完整语法 -->
<a v-on:click="doSomething"></a>
<!-- 缩写 -->
<a @click="doSomething"></a>


# 循环语句
v-for

## v-for 迭代对象

### 一个参数
<!-- 遍历的value值 -->
<li v-for="value in object">
{{ value }}
</li>

### 两个参数
<!-- 📢 注意：value在前，key在后 -->
v-for="(value,key) in object"

### 三个参数
v-for="(value, key, index) in object"

## v-for 迭代整数
v-for="n in 10"

## 显示过滤/排序后的结果
<!-- computed：计算属性 -->

<li v-for="n in evenNumbers">{{ n }}</li>

<script>
const app = {
    data() {
        return {
            numbers: [ 1, 2, 3, 4, 5 ]
	     }
    },
    computed: {
        evenNumbers() {
            return this.numbers.filter(number => number % 2 === 0)
        }
    }
}
 
Vue.createApp(app).mount('#app')
</script>


# 组件

## 全局组件

注册一个全局组件：
const app = Vue.createApp({...})

app.compoment('my-component-name', {
  data() {
    return {
      count: 0
    }
  },
  template: `
    <button @click="count++">
      点了 {{ count }} 次！
    </button>`
})

使用：
<my-component-name></my-component-name>

注意：template 中 ` 是反引号，不是单引号 '。

## 局部组件
const ComponentA = {
  /* ... */
}

const app = Vue.createApp({
  components: {
    'component-a': ComponentA,
    'component-b': ComponentB
  }
})

## Prop
属性：组件传值
props: ['title'],

### 动态 Prop
父类用v-bind

### Prop 验证
props: {
    // 基础的类型检查 (`null` 和 `undefined` 会通过任何类型验证)
    propA: Number,
    // 多个可能的类型
    propB: [String, Number],
    // 必填的字符串
    propC: {
      type: String,
      required: true
    },
    // 带有默认值的数字
    propD: {
      type: Number,
      default: 100
    },
    // 带有默认值的对象
    propE: {
      type: Object,
      // 对象或数组默认值必须从一个工厂函数获取
      default: function () {
        return { message: 'hello' }
      }
    },
    // 自定义验证函数
    propF: {
      validator: function (value) {
        // 这个值必须匹配下列字符串中的一个
        return ['success', 'warning', 'danger'].indexOf(value) !== -1
      }
    }
  }

type 可以是下面原生构造器：

String
Number
Boolean
Array
Object
Date
Function
Symbol
type 也可以是一个自定义构造器，使用 instanceof 检测。


# Vue3 计算属性
computed

computed: {
    // 计算属性的 getter
    reversedMessage: function () {
      // `this` 指向 vm 实例
      return this.message.split('').reverse().join('')
    }
}

性能：computed > methods

## getter setter

computed: {
    site: {
      // getter
      get: function () {
        return this.name + ' ' + this.url
      },
      // setter
      set: function (newValue) {
        var names = newValue.split(' ')
        this.name = names[0]
        this.url = names[names.length - 1]
      }
    }

# Vue3 监听属性
watch

vm = Vue.createApp(app).mount('#app')
vm.$watch('counter', function(nval, oval) {
  alert('计数器值的变化 :' + oval + ' 变为 ' + nval + '!');
})

# Vue3 样式绑定
v-bind:xxx
:xxx


## class 属性绑定
<div class="static" :class="{ 'active' : isActive, 'text-danger' : hasError }">
</div>

也可以通过computed返回一个样式
<div id="app">
    <div class="static" :class="classObject"></div>
</div>

computed: {
  classObject() {
    return {
      active: this.isActive,
      'text-danger': this.error
    }
  }
}

## 数组语法
<div class="static" :class="[activeClass, errorClass]"></div>

三元表达式
<div id="app">
    <div class="static" :class="[isActive ? activeClass : '', errorClass]"></div>
</div>

## Vue.js style(内联样式)
v-bind:style / :style

<div :style="{ color: activeColor, fontSize: fontSize + 'px' }">菜鸟教程</div>

绑定样式对象
<div :style="styleObject">菜鸟教程</div>

<div :style="[baseStyles, overridingStyles]">菜鸟教程</div>

## 多重值
常用于提供多个带前缀的值
<div :style="{ display: ['-webkit-box', '-ms-flexbox', 'flex'] }"></div>

## 组件上使用 class 属性

当你在带有单个根元素的自定义组件上使用 class 属性时，这些 class 将被添加到该元素中。此元素上的现有 class 将不会被覆盖。

<runoob class="classC classD"></runoob>

$attrs：定义哪些部分将接收这个类

app.component('runoob', {
  template: `
    <p :class="$attrs.class">I like runoob!</p>
    <span>这是一个子组件</span>
  `
})


# Vue3 事件处理
v-on:xxx / @xxx

事件处理程序中可以有多个方法，这些方法由逗号运算符分隔
<!-- 这两个 one() 和 two() 将执行按钮点击事件 -->
<button @click="one($event), two($event)"> 点我 </button>

## 事件修饰符

.stop - 阻止冒泡
.prevent - 阻止默认事件
.capture - 阻止捕获
.self - 只监听触发该元素的事件
.once - 只触发一次
.left - 左键事件
.right - 右键事件
.middle - 中间滚轮事件

<!-- 阻止单击事件冒泡 -->
<a v-on:click.stop="doThis"></a>
<!-- 提交事件不再重载页面 -->
<form v-on:submit.prevent="onSubmit"></form>
<!-- 修饰符可以串联  -->
<a v-on:click.stop.prevent="doThat"></a>
<!-- 只有修饰符 -->
<form v-on:submit.prevent></form>
<!-- 添加事件侦听器时使用事件捕获模式 -->
<div v-on:click.capture="doThis">...</div>
<!-- 只当事件在该元素本身（而不是子元素）触发时触发回调 -->
<div v-on:click.self="doThat">...</div>

<!-- click 事件只能点击一次，2.1.4版本新增 -->
<a v-on:click.once="doThis"></a>

## 按键修饰符

<!-- 只有在 keyCode 是 13 时调用 vm.submit() -->
<input v-on:keyup.13="submit">

常用keyCod：
<!-- 同上 -->
<input v-on:keyup.enter="submit">
<!-- 缩写语法 -->
<input @keyup.enter="submit">

全部的按键别名：

.enter
.tab
.delete (捕获 "删除" 和 "退格" 键)
.esc
.space
.up
.down
.left
.right
系统修饰键：

.ctrl
.alt
.shift
.meta
鼠标按钮修饰符:

.left
.right
.middle

.exact 修饰符

<!-- 即使 Alt 或 Shift 被一同按下时也会触发 -->
<button @click.ctrl="onClick">A</button>

<!-- 有且只有 Ctrl 被按下的时候才触发 -->
<button @click.ctrl.exact="onCtrlClick">A</button>

<!-- 没有任何系统修饰符被按下的时候才触发 -->
<button @click.exact="onClick">A</button>

# Vue3 表单

## 复选框

复选框如果是一个为逻辑值，如果是多个则绑定到同一个数组：
单选
<input type="checkbox" id="checkbox" v-model="checked">
<label for="checkbox">{{ checked }}</label>
多选
<input type="checkbox" id="runoob" value="Runoob" v-model="checkedNames">
<label for="runoob">Runoob</label>
<input type="checkbox" id="google" value="Google" v-model="checkedNames">
<label for="google">Google</label>

## 单选按钮

<input type="radio" id="runoob" value="Runoob" v-model="picked">
<label for="runoob">Runoob</label>

## select 列表

<select v-model="selected" name="site">
  <option value="">选择一个网站</option>
  <option value="www.runoob.com">Runoob</option>
  <option value="www.google.com">Google</option>
</select>

## 值绑定

### 复选框 (Checkbox)：

<input type="checkbox" v-model="toggle" true-value="yes" false-value="no" />
...
// 选中时
vm.toggle === 'yes'
// 取消选中 
vm.toggle === 'no'

### 单选框 (Radio)：

<input type="radio" v-model="pick" v-bind:value="a" />
// 当选中时
vm.pick === vm.a

### 选择框选项 (Select)：
<select v-model="selected">
  <!-- 内联对象字面量 -->
  <option :value="{ number: 123 }">123</option>
</select>
// 当被选中时
typeof vm.selected // => 'object'
vm.selected.number // => 123

## 修饰符

### .lazy
<!-- 在 "change" 而不是 "input" 事件中更新 -->
<input v-model.lazy="msg" >

### .number
<input v-model.number="age" type="number">

### trim
<input v-model.trim="msg">
