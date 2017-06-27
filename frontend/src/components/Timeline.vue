<template>
  <div class="timeline">
    <feed :tweets="tweets"/>
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
