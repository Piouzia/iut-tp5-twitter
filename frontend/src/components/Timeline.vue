<template>
  <div class="timeline">
    <ul>
      <li v-for="tweet in tweets"><tweet :tweet="tweet"/></li>
    </ul>
  </div>
</template>

<script>
var tweet1 = {auteur: 'auteur1', contenu: 'voilà un super contenu !'}
var tweet2 = {auteur: 'auteur2', contenu: 'Wouah tip top !'}
var tweet3 = {auteur: 'auteur3', contenu: 'On s\'éclate sur Twitter yahou !'}
import Tweet from './Tweet'
export default {
  name: 'timeline',
  components: {Tweet},
  data () {
    return {
      tweets: [tweet1, tweet2, tweet3]
    }
  }
}
</script>


<style scoped>
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: block;
  margin: 0 10px;
}
</style>
