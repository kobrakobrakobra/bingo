<template>
  <div id="app">
    <AppHeader></AppHeader>
    <router-view/>
<!-- <AppFooter></AppFooter> -->
  </div>
</template>

<script>
  import AppHeader from './components/AppHeader'
  //import AppFooter from './components/AppFooter'

  export default {
    components: {
      AppHeader,
    //AppFooter
    }
  }
</script>

<style>

body {
  background-color: #eceff6;
  font-family: 'Open Sans', sans-serif;
}

.notouch {
  user-select: none;
}

#app {
  display: flex;
  min-height: 100vh;
  flex-direction: column;
  font-family: 'Open Sans', sans-serif;
}

#app > .app-content {
  flex: 1 0 auto;
}
</style>

