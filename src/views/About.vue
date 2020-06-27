<template>
  <div class="about">
    <h1>This is an about page</h1>
    <div>二哈：{{obj.name}}{{age}} ----toRefs 二哈：{{name}}{{age}}</div>
    <button @click="changeJackAge">Change Jack Age</button>
    <div v-for="(item,index) in list" :key="item.age+index">{{item.name}}今年{{item.age}}岁</div>

    <button @click="toRefsChangeAge()">toRefsChangeAge</button>
  </div>
</template>
<script>
import { reactive, toRefs } from 'vue'
export default {
  name: 'about',
  setup () {
    const dataList = [
      {
        name: 'lisa',
        age: 19
      },
      {
        name: '张三',
        age: 21
      },
      {
        name: 'jack',
        age: 23
      }
    ]
    const objData = {
      name: 'erha',
      age: '1',
      skill: '拆家'
    }
    const obj = reactive(objData) // 定义响应式数据obj
    const list = reactive(dataList) // 定义响应式数据list
    const changeJackAge = () => {
      // console.log(list)
      list[2].age = 34
    }
    const { name, age } = toRefs(obj)
    const toRefsChangeAge = () => {
      // console.log(age)
      age.value = 1000
    }
    return {
      list,
      changeJackAge,
      obj,
      name,
      age,
      toRefsChangeAge
      // ...toRefs(obj) // 转换
    }
  }
}
</script>
