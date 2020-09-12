<template>
  <v-container class="justify-center">
    <v-row dense>
      <v-col cols="12">
        <v-card
          height="80px"
          min-width="290px"
          class="d-flex align-center"
          elevation="5"
        >
          <v-col cols="3" class="justify-center">
            <v-row justify="center">
              <v-avatar>
                <img
                  :src="superheroe.avatarURL"
                >
              </v-avatar>
            </v-row>
          </v-col>
          <v-col cols="9">
            <v-card-title secondary-title>
              <div>
                <div class="subheading blue-grey--text">
                  {{ superheroe.nombre }}
                </div>
                <span class="grey--text">{{ superheroe.nombreReal }}</span>
              </div>
            </v-card-title>
          </v-col>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>
<script>
export default {
  name:
    'CardSuperheroe',
  props: [
    // eslint-disable-next-line
    'superheroe'
  ],
  created () {
    this.validateAvatar()
    this.validateData()
  },
  methods: {
    async validateAvatar () {
      const proxy = 'https://images1-focus-opensocial.googleusercontent.com/gadgets/proxy?container=focus&refresh=2592000&url='
      const img = this.superheroe.avatarURL
      await this.$axios.$get(proxy + img)
        .catch((err) => {
          if ([403, 404, 500].includes(err.response.status)) {
            this.superheroe.avatarURL = 'https://static.thenounproject.com/png/55168-200.png'
            this.$emit('update_errors', 'La imagen tiene problemas, por lo que se usa una por defecto')
          }
        })
    },
    validateData () {
      if (this.superheroe.nombre === undefined || this.superheroe.nombre === null) {
        this.$emit('update_errors', 'No existe campo nombre, por lo que se llama indefinido')
        this.superheroe.nombre = 'Desconocido'
      }
      if (this.superheroe.nombreReal === undefined || this.superheroe.nombreReal === null) {
        this.$emit('update_errors', 'No existe campo nombreReal, por lo que se llama indefinido')
        this.superheroe.nombreReal = 'Desconocido'
      }
      if (this.superheroe.avatarURL === undefined || this.superheroe.avatarURL === null) {
        this.$emit('update_errors', 'No existe campo avatarURL, por lo que se pone una imagen predeterminada')
        this.superheroe.avatarURL = 'https://static.thenounproject.com/png/55168-200.png'
      }
    }
  }
}
</script>
