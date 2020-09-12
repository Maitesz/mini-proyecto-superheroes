<template>
  <v-container fluid>
    <v-row justify="center">
      <v-col xs="12" md="10">
        <v-text-field
          id="input-search"
          v-model="searchTitle"
          label="Buscar por nombre"
          outlined
        />
      </v-col>
    </v-row>
    <v-row justify="center">
      <v-col cols="10">
        <v-row>
          <v-col
            v-for="(superheroe, index) in superheroesFilter"
            :key="index"
            v-model="superheroes"
            xs="12"
            md="6"
            lg="4"
          >
            <cardSuperheroe :superheroe="superheroe" @update_errors="update($event)" />
          </v-col>
        </v-row>
      </v-col>
      <v-col cols="12">
        <v-divider class="pa-2 mt-2" />
      </v-col>
      <v-col cols="8">
        <v-alert
          v-for="(errorcito, index) in errorsData"
          :key="index"
          v-model="alert"
          color="error"
          dismissible
        >
          {{ errorcito }}
        </v-alert>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import cardSuperheroe from '../components/CardSuperheroe'
export default {
  name: 'Superheroes',
  components: { cardSuperheroe },
  async asyncData ({ $axios }) {
    const errores = []
    const superheroes = await $axios.get('/superheroes?puedeVolar=true')
      .catch((err) => {
        if (err.response && err.response.status) {
          errores.push('Error al buscar los superheroes que vuelan, código: ', err.response.status)
        }
      })
    const heroId = await $axios.get('/superheroes/1')
      .catch((err) => {
        if (err.response && err.response.status) {
          errores.push('Error al buscar el superhéroe con ID = 1, código: ', err.response.status)
        }
      })
    return {
      superheroes: superheroes.data.data,
      hero1: heroId.data.data,
      errorsData: errores
    }
  },
  data: () => ({
    superheroes: [],
    hero1: {},
    searchTitle: '',
    errorsData: []
  }),
  computed: {
    superheroesFilter () {
      if (this.superheroes !== [] && this.superheroes !== undefined) {
        return this.superheroes.filter((superheroe) => {
          return superheroe.nombre.toLowerCase().match(this.searchTitle.toLowerCase())
        })
      }
      return []
    }
  },
  created () {
    if (this.superheroes !== [] && this.hero1 !== {}) {
      this.superheroes.push(this.hero1)
    }
  },
  methods: {
    update (v) {
      // this.$router.push('/project/' + v.id)
      this.errorsData.push(v)
    }
  }
}

</script>

<style scoped>

</style>
