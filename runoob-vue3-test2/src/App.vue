<template>
  <img alt="Vue logo" src="./assets/logo.png" />
  <HelloWorld msg="欢迎来到菜鸟教程！" />

  <h2>Vue3 表单</h2>

  <!-- 当选中时，`picked` 为字符串 "a" -->
  <input type="radio" v-model="picked" value="a" />
  <input type="radio" v-model="pick" v-bind:value="a" />
  <div>picked: {{ picked }}</div>
  <div>pick: {{ pick }}</div>
  <div>a: {{ a }}</div>

  <!-- `toggle` 为 true 或 false -->
  <input type="checkbox" v-model="toggle" />
  <input type="checkbox" v-model="toggle" true-value="yes" false-value="no" />
  <div>toggle: {{ toggle }}</div>

  <!-- 当选中第一个选项时，`selected` 为字符串 "abc" -->
  <select v-model="selected">
    <option value="abc">ABC</option>
  </select>
  <br>

  <select v-model="selected">
    <!-- 内联对象字面量 -->
    <option :value="{ number: 123 }">123</option>
  </select>

  <div>选择的是: {{ selected }}</div>

  <h3>修饰符</h3>

  <li>.lazy</li>

  <!-- 在 "change" 而不是 "input" 事件中更新 -->
  <input v-model.lazy="msg">
  <div>msg: {{ msg }}</div>

  <li>.number</li>

  <input v-model.number="age" type="number">
  <div>age: {{ age }}</div>

  <li>.trim</li>

  <input v-model.trim="msg">

</template>

<script>
import HelloWorld from './components/HelloWorld.vue'

export default {
  data () {
    return {
      age: NaN,
      msg: '',
      picked: '',
      pick: '',
      a: '123',
      toggle: '',
      selected: ''
    }
  },
  name: 'App',
  components: {
    HelloWorld
  }
}
</script>