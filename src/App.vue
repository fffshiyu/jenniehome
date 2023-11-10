<template>
  <HelloWorld />
  <ThreePart />
  <DonatPart />
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import ThreePart from './components/ThreePart.vue'
import DonatPart from './components/DonatPart.vue'


export default {
  name: 'App',
  components: {
    HelloWorld,
    ThreePart,
    DonatPart
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  overflow-x: hidden;


}
</style>
