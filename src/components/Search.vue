<template lang="html">
  <v-container>
    <v-form>
      <v-layout>
        <v-flex xs12 md4>
          <v-text-field
            v-model="query"
            label="Artist name"
            required
          ></v-text-field>
        </v-flex>
      </v-layout>
      <v-layout>
        <v-btn color="success" @click="search">Search</v-btn>
      </v-layout>
    </v-form>
    <v-layout>
      <v-flex xs12 sm6 offset-sm3>
        <v-card>
          <v-img
            src="https://cdn.vuetifyjs.com/images/cards/desert.jpg"
            aspect-ratio="2.75"
          ></v-img>
          <v-card-title primary-title>
            <div>
              <h3 class="headline mb-0">Kangaroo Valley Safari</h3>
              <div>Located two hours south of Sydney in the <br>Southern Highlands of New South Wales, ...</div>
            </div>
          </v-card-title>
          <v-card-actions>
            <v-btn flat color="orange">Share</v-btn>
            <v-btn flat color="orange">Explore</v-btn>
          </v-card-actions>
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
      results: []
    }
  },
  methods: {
    search () {
      spotify.search(this.query, 'artist')
        .then((res) => {
          this.results = res.artists.items
          console.log(this.results)
        })
    }
  }
}

</script>
