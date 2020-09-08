<template>
  <div id="app">
    <home />
  </div>
</template>

<script>
import home from './components/home'

export default {
  name: 'App',
  components: {
    home
  }
}
</script>

<style lang="sass">
*
  margin: 0
  padding: 0
  
#app
  font-family: sans-serif
  height: 100vh
  width: 100vw
  background: #303030
</style>
