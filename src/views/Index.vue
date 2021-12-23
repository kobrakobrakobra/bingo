<template>
  <div class="app-content">
    <bingo></bingo>
  </div>
</template>

<script>
import Bingo from '../components/Bingo'

export default {
  name: 'home',
  components: {
    Bingo,
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Open+Sans:wght@300;400;500;600;700;800&display=swap');

html {
 font-family: "Open Sans", sans-serif;
}

</style>
