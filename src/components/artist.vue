<template lang = "pug">
  li
    img(class="img" :src="artist.image[4]['#text']")
    h2: a(:href="artist.url" target="_blank") {{ artist.name }}
</template>

<script>
export default {
  name: 'artist',
  props: ['artist']
}
</script>

<style lang="stylus">
  li
    display block
    margin 10 0px

  .img 
    width 30%
    border 3px black outset

</style>