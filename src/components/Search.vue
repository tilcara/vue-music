<template lang="html">
  <v-container>
    <v-form v-model="valid">
      <v-layout>
        <v-flex xs12 md4>
          <v-text-field
            v-model="query"
            label="Artist name"
            required
            @keyup.enter="search"
            :rules="nameRules"
          ></v-text-field>
        </v-flex>
      </v-layout>
      <v-layout>
        <v-btn color="success" @click="search">Search</v-btn>
        <v-btn color="error" @click.prevent="reset">Clean</v-btn>
      </v-layout>
    </v-form>
    <v-layout>
      <v-flex xs12 sm6 offset-sm3>
        <small>{{ found }}</small>
        <div class="text-xs-center" v-show="isLoading">
          <v-progress-circular
            :size="70"
            :width="7"
            color="purple"
            indeterminate
          ></v-progress-circular>
        </div>
        <h2 v-if="results.length === 0">
          No results found
        </h2>
        <v-card v-for="result in results" :key="result.id">
          <v-img
            v-if="result.images.length"
            :src="result.images[0].url"
            :alt="result.name"
            aspect-ratio="2.75"
          ></v-img>
          <v-card-title primary-title>
            <div>
              <h3 class="headline mb-0">{{ result.name }}</h3>
            </div>
          </v-card-title>
          <v-card-actions>
            <v-btn :href="result.external_urls.spotify" flat color="orange" target="_blank">Abrir en el explorador</v-btn>
            <v-btn :href="result.uri" flat color="orange">Abrir en la app</v-btn>
          </v-card-actions>
          <hr><hr><hr>
        </v-card>
      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
import spotify from '../services/spotify.js'

export default {
  name: 'Search',
  data () {
    return {
      query: '',
      results: [],
      isLoading: false,
      valid: false,
      nameRules: [
        v => !!v || 'Name is required'
      ]
    }
  },
  methods: {
    search () {
      if (this.query !== '') {
        this.isLoading = true
        spotify.search(this.query, 'artist')
          .then((res) => {
            this.results = res.artists.items
            console.log(this.results)
            this.isLoading = false
          })
      }
    },
    reset () {
      this.query = ''
      this.results = []
    }
  },
  computed: {
    found () {
      return this.results.length
        ? `${this.results.length} results` : ''
    }
  },
  watch: {
    query (newData, oldData) {
      console.log(newData)
    }
  }
}

</script>

<style lang="stylus" scoped>
  .v-progress-circular
    margin: 1rem
</style>
