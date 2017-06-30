<template>
  <div class="feed">

    <div v-if="loading">
      Chargement des tweets en cours…
    </div>
    <div v-else>
      <ul>
        <li class="tweet" v-for="tweet in tweets"><tweet @retweeted="retweet" :tweet="tweet" :currentUser="currentUser"/></li>
      </ul>
    </div>
  </div>
</template>

<script>
import Vue from 'vue'
import Resource from 'vue-resource'
Vue.use(Resource)
import Tweet from './Tweet'
export default {
  name: 'feed',
  components: {Tweet},
  props: ['tweets', 'loading', 'currentUser'],
  methods: {
    retweet: function (id) {
      this.$emit('retweeted', id)
    }
  },
  data () {
    return {
    }
  }
}
</script>


<style scoped>

li.tweet:first-child {
 border-top-width: 1px;
}

li.tweet {
 border-style: solid;
 border-width: 0 1px 1px 1px;
 border-color: gray;
 width: 500px;
 margin: auto;
}

ul {
  list-style-type: none;
  padding: 0;
}
</style>
