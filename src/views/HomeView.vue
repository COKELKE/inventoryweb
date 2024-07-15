<template>
  <div class="home">
    <!-- <img alt="Vue logo" src="../assets/logo.png"> -->
    <!-- <HelloWorld msg=""/> -->
    <home msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
// @ is an alias to /src
 //import HelloWorld from '@/components/HelloWorld.vue'
//import PaginatedBookings from '@/components/home.vue'
import home from '@/components/home.vue'

export default {
  name: 'HomeView',
  components: {
    //HelloWorld
    //PaginatedBookings
    home
  }
}
</script>