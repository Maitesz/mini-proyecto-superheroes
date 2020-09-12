<template>
  <v-app >
    <Banner/>
    <Nuxt />
  </v-app>
</template>

<script>
import Banner from '../components/Banner'
export default {
  components: { Banner },
  data () {
    return {
      fixed: false
    }
  }
}
</script>

<style>
  .parallax {
    background-color: darkblue;
    background-size:cover;
    /* Set a specific height */
    min-height: 100vh;
    /* Create the parallax scrolling effect */
    background-position: center;
    background-repeat: repeat-y;
    background-size: cover;
  }
</style>
