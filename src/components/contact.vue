<template>
  <div class="home">
    <h1 class="pt-4">Contact us</h1>
    <app-form></app-form>
  </div>

</template>
<script>
import Form from './form.vue';
export default {
  name: 'contact',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
  },
  components: {
    'app-form': Form
  }
}
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
