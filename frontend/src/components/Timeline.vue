<template>
  <div class="timeline">
    <Utilisateurs @changeUtilisateur="changeUtilisateur"/>
    <feed :tweets="tweets" @retweeted="retweet" :loading="loading" :currentUser="currentUser"/>
  </div>
</template>

<script>
import Vue from 'vue'
import Resource from 'vue-resource'
Vue.use(Resource)
import Utilisateurs from './Utilisateurs'
import Feed from './Feed'
export default {
  name: 'timeline',
  components: {Feed, Utilisateurs},
  methods: {
    fetchTweets: function () {
      this.$http.get('http://localhost:8080/list').then(response => {
        this.tweets = response.body
        this.loading = false
      }, response => {
        console.log('error')
      })
    },
    retweet: function (id) {
      var tweet = this.tweets.find(e => e.id === id)
      var handle = this.tweets.find(e => e.handle === handle)
      tweet.retweeters.push({handle: handle})
    },
    changeUtilisateur: function (handle) {
      this.currentUser = handle
    }
  },
  created () {
    this.fetchTweets()
  },
  data () {
    return {
      loading: true,
      tweets: [],
      currentUser: 'test'
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
