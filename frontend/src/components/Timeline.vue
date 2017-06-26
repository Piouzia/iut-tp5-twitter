<template>
  <div class="timeline">
    <ul>
      <li v-for="tweet in tweets"><tweet :tweet="tweet"/></li>
    </ul>
  </div>
</template>

<script>
import Vue from 'vue'
import Resource from 'vue-resource'
Vue.use(Resource)
var tweet1 = {auteur: 'auteur1', contenu: 'voilà un super contenu !'}
var tweet2 = {auteur: 'auteur2', contenu: 'Wouah tip top !'}
var tweet3 = {auteur: 'auteur3', contenu: 'On s\'éclate sur Twitter yahou !'}
import Tweet from './Tweet'
export default {
  name: 'timeline',
  components: {Tweet},
  created () {
   this.fetchTweets()
  },
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
