<template lang="pug">
  li.artista
    h2: a(:href="artista.url" target="_blank") {{ artista.name}}
    img(:src="artista.image[2]['#text']")
</template>

<script>
export default {
  name: 'Artista',
  props: ['artista']

}
</script>

<style lang="stylus" scoped>
  li.artista
    display block
    margin 10px 0
</style>
