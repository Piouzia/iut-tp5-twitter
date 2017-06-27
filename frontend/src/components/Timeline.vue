<template>
  <div class="timeline">
    <feed :tweets="tweets" :loading="loading"/>
  </div>
</template>

<script>
import Vue from 'vue'
import Resource from 'vue-resource'
Vue.use(Resource)
import Feed from './Feed'

export default {
  name: 'timeline',
  components: {Feed},
  methods: {
    fetchTweets: function () {
      this.$http.get('http://localhost:8080/list').then(response => {
        this.tweets = response.body
        this.loading = false
      }, response => {
        console.log('error')
      })
    }
  },
  created () {
    this.fetchTweets()
  },
  data () {
    return {
      loading: true,
      tweets: []
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
