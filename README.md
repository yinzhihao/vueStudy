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