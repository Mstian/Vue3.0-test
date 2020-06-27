<template>
  <div class="test">
    <img alt="Vue logo" src="../assets/logo.png">
    <div>欢迎体验Vue3.0呀</div>
    <div class="count"> count : {{count}}</div>
    <div>计算属性: doubleCount : {{doubleCount}}</div>
    <div>watch: count+num：{{countAddNum}}</div>
    <button @click="addCount">点击+1</button>
    <button @click="pushRoute">编程导航</button>
  </div>
</template>

<script>
import { ref, computed, watch, getCurrentInstance } from 'vue'
export default {
  setup () {
    // ctx相当于this
    const { ctx } = getCurrentInstance() // 获取当前组件上下文 类似于vue2.0中的this
    console.log(ctx)// 与2.0项目中的this作比较观察
    // 相当于data
    const count = ref(0) // 定义响应式数据count
    const num = ref(1) // 定义响应式数据num
    // 相当于computed
    const doubleCount = computed(() => { // 计算属性每次count增加2
      return count.value * 2
    })
    const countAddNum = computed(() => { // 计算属性
      return count.value + num.value
    })
    // 相当于watch
    watch(
      [() => count.value, () => num.value],
      ([count, num], [oldCount, oldNum]) => { // watch 同时观察count和num两个值
        console.log(`count:${count},num:${num} oldCount:${oldCount},oldNum:${oldNum}`)
      })
    watch(() => { return count.value }, (newcount) => {
      console.log('count变啦', newcount)
    })
    // 相当于methods
    const addCount = () => { // 定义增加count方法
      count.value++
    }
    const pushRoute = () => { // 编程导航
      ctx.$router.push({
        path: '/about'
      })
    }
    // 统一return出去
    return {
      count,
      addCount,
      doubleCount,
      num,
      countAddNum,
      pushRoute
    }
  },
  name: 'Test',
  components: {
  },
  mounted () {
    // console.log(this.$router.currentRoute.value)
  }
  // 参考文章
  // https://juejin.im/post/5bfcbab0518825741e7bd67f Proxy
  // https://www.cnblogs.com/yf-html/p/12753540.html vue cli体验vue3.0
  // https://juejin.im/post/5eb17a0fe51d454dd60cfe0f Composition API
  // https://juejin.im/post/5e8010e26fb9a03c947cb98d
  // https://juejin.im/post/5e16e800f265da3e1824b72c Vue3改动地方
  /**
   使用 Typescript
   放弃 class 采用 function-based API
   option API => Composition API
   重构 complier
   重构 virtual DOM
   新的响应式机制
   */
  // https://zhuanlan.zhihu.com/p/37404624
  // https://www.jianshu.com/p/1d5bcc0e3447
}
</script>
