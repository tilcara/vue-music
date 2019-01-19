<template>
  <v-app>
    <v-toolbar app>
      <v-toolbar-title class="headline text-uppercase">
        <span>Search Music 🎵</span>
      </v-toolbar-title>
    </v-toolbar>

    <v-content>
      <search/>
    </v-content>
  </v-app>
</template>

<script>
import Search from './components/Search'

export default {
  name: 'App',
  components: {
    Search
  },
  data () {
    return {
      //
    }
  }
}
</script>
