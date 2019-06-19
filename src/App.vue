<template lang="pug">
  #app
    img(src='../dist/logo.png' width="150")
    h1 {{ titulo }}
    select(v-model="paisSelect")
      option(v-for="pais in paises" :value="pais.value") {{ pais.name}}
    Spinner(v-show="cargando")
    ul
      Artista(v-for="artista in artistas" :artista="artista" :key="artista.mbid")
</template>

<script>
import Spinner from '../components/Spinner.vue'
import Artista from '../components/Artista.vue'
import getArtistas from './api'

export default {
  name: 'app',
  data () {
    return {
      titulo: 'PhoenixMusic',
      artistas: [],
      paises: [
        {name: 'Venezuela', value: 'Venezuela'},
        {name: 'Colombia', value: 'Colombia'},
        {name: 'Argentina', value: 'Argentina'},
        {name: 'España', value: 'Spain'}
      ],
      paisSelect: 'Venezuela',
      cargando: true
    }
  },
  components: {
    Artista,
    Spinner
  },
  methods: {
    refreshArtista(){
      const self = this
      this.cargando = true
      this.artistas = []
      getArtistas(this.paisSelect)
      .then(function(artist){
        self.cargando = false
        self.artistas = artist
      })
    }
  },
  mounted: function(){
    this.refreshArtista()
  },
  watch: {
    paisSelect: function () {
      this.refreshArtista()
    }
  }
}
</script>

<style lang="stylus">
#app
	font-family 'Avenir', Helvetica, Arial, sans-serif
	-webkit-font-smoothing antialiased
	-moz-osx-font-smoothing grayscale
	text-align center
	color #fa6405
	margin-top 60px
h1, h2
	font-weight normal
ul
	list-style-type none
	padding 0
li
	display inline-block
	margin 0 10px
a
	color #fa6405

</style>
