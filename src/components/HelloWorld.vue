<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <div>{{a}}</div>
    <button @click="setA">加A</button>
  </div>
</template>

<script>
import {
  ref,
  onBeforeMount,
  onMounted,
  onBeforeUpdate,
  onUpdated,
  onBeforeUnmount,
  onUnmounted,
  onErrorCaptured,
  onRenderTracked,
  onRenderTriggered
} from 'vue'
export default {
  setup (props, context) {
    // console.log(props.msg, context)
    const a = ref(0)
    const setA = () => {
      return a.value++
    }
    // 相当于 beforeMount
    onBeforeMount(() => {
      console.log('onBeforeMount')
    })
    // 相当于 mounted
    onMounted(() => {
      console.log('onMounted')
    })
    // 相当于 beforeUpdate
    onBeforeUpdate(() => {
      console.log('onBeforeUpdate')
    })
    // 相当于 updated
    onUpdated(() => {
      console.log('onUpdated')
    })
    // 相当于 beforeDestroy
    onBeforeUnmount(() => {
      console.log('onBeforeUnmount')
    })
    // 相当于 destroyed
    onUnmounted(() => {
      console.log('onUnmounted')
    })
    onErrorCaptured(() => { // 错误监控 参考文章 https://zhuanlan.zhihu.com/p/37404624
      console.log('onErrorCaptured')
    })
    onRenderTracked(() => { // 已渲染
      console.log('onRenderTracked')
    })
    onRenderTriggered(() => { // 当组件更新时会首先触发此生命周期钩子 onRenderTriggered->onRenderTracked->onBeforeUpdate->onUpdated
      console.log('onRenderTriggered')
    })
    return {
      a,
      setA
    }
  },
  name: 'HelloWorld',
  props: {
    msg: String
  }
}
</script>
