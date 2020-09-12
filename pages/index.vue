<template>
  <v-container >
    <v-row justify="center">
      <v-col>
        <v-btn block color="primary" @click="go">
          Ir a Superhéroes
        </v-btn>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>

export default {
  methods: {
    go () {
      this.$router.push('/superheroes')
    }
  }
}
</script>
