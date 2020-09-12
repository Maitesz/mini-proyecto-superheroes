<template>
  <v-container fluid fill-height>
    <v-row>
      <v-col cols="12">
        <img width="100%" height="500" class="banner" :src="require(`@/assets/super.jpg`)">
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  name: 'Banner'
}
</script>

<style scoped>
.banner{
  background-repeat: repeat-y;
}
</style>
