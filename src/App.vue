<template lang = "pug">
#app
  img(src='https://jonhks.github.io/api-music-vue/dist/logo.png')
  h1 Api Music
  select(v-model="selectedCountry")
    option(v-for="country in countries" v-bind:value="country.value") {{ country.name }}
  spinner(v-show="loading")
  ul
    artist(v-for="artist in artists" v-bind:artist="artist" v-bind:key="artist.mbid")
    
</template>

<script>

import artist from "./components/artist.vue";
import Spinner from './components/Spinner.vue';
import getArtists from "./api";

export default {
  name: "app",
  data() {
    return {
      artists: [],
      countries: [
        { name: "Argentina", value: "argentina" },
        { name: "Colombia", value: "colombia" },
        { name: "España", value: "spain" },
        { name: "Mexico", value: "mexico" },
        { name: "Brazil", value: "brazil" },

      ],
      selectedCountry: "canada", 
      loading: true
    };
  },
  components: {
    artist,
    Spinner
  },
  methods: {
    refreshArtists () {
      this.loading = true
      const self = this
      this.artists = []
      const newSelect = this.selectedCountry
      getArtists(newSelect)
      .then(function(artists) {
        self.loading = false
        self.artists = artists
      });

    }
  },
  mounted: function () {
    this.refreshArtists()
  },
  watch: {
    selectedCountry() {
     this.refreshArtists()
    }
  }
};
</script>

<style lang="stylus">
#app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 40px;
}

h1, h2 {
    font-weight: normal;
}

ul {
    list-style-type: none;
    padding: 0;
}

li {
    display: inline-block;
    margin: 0 10px;
}

a {
    color: #42b983;
}
</style>
