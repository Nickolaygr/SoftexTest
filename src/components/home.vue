<template>
  <div class="home">
    <h1 class="pt-4">Home</h1>
    <carousel  class="pt-3" :margin="10" :autoplay="true" :items="3" :loop="true" :responsive="{0:{items:1,nav:false},500:{items:2,nav:true},800:{items:3,nav:true}}">
      <router-link to="/about"><img src="https://placeimg.com/200/200/any?1"></router-link>
      <router-link to="/about"><img src="https://placeimg.com/200/200/any?2"></router-link>
      <router-link to="/about"><img src="https://placeimg.com/200/200/any?3"></router-link>
      <router-link to="/about"><img src="https://placeimg.com/200/200/any?4"></router-link>
      <router-link to="/about"><img src="https://placeimg.com/200/200/any?5"></router-link>
      <router-link to="/about"><img src="https://placeimg.com/200/200/any?6"></router-link>
      <router-link to="/about"><img src="https://placeimg.com/200/200/any?7"></router-link>
    </carousel>
  </div>

</template>

<script>
import carousel from 'v-owl-carousel'
export default {
  name: 'home',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
  },
  components: { carousel }
}
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
