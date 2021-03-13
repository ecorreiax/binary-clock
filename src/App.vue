<template>
  <div class="container">
    <vClock/>
  </div>
</template>

<script>
import vClock from './components/Clock.vue'

export default {
  name: 'App',
  components: {
    vClock
  }
}
</script>

<style lang="scss" src="@/assets/style.scss">
</style>
