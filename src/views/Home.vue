<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'
import { onErrorCaptured } from 'vue'
export default {
  setup () {
    onErrorCaptured((err, vm, info) => { // 捕获子孙组件的错误,err:错误对象 vm:发生错误的vuez组件实例 info:Vue特定错误信息，比如发生错误的生命周期
      console.log('onErrorCaptured', err, vm, info)
    })
  },
  name: 'Home',
  components: {
    HelloWorld
  }
}
</script>
