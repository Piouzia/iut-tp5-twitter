<template>
  <div class="tweet">
    <div>
      <strong>{{ tweet.auteur.prenom }} {{ tweet.auteur.nom }}</strong> <span class="handle">@{{ tweet.auteur.handle }}</span> - {{moment(tweet.date).fromNow()}}
    </div>
    <div>
      {{ tweet.contenu }}
    </div>
    <div>
      <ul>
        <li class="button"> <icon name="reply"/> </li>
        <a @click="retweet()"><li class="button"> <icon name="retweet"/> {{ countRetweet() }} </li></a>
        <li class="button"> <icon name="heart"/> </li>
        <li class="button"> <icon name="envelope"/> </li>
      </ul>
    </div>
  </div>
</template>

<script>
import 'vue-awesome/icons'
import Icon from 'vue-awesome/components/Icon'
import moment from 'moment'
export default {
  name: 'tweet',
  components: {Icon},
  methods: {
    moment: function (date) {
      return moment(date)
    },
    countRetweet: function () {
      return this.tweet.retweeters.length
    },
    retweet: function () {
      this.$http.get('http://localhost:8080/retweet', {params: {utilisateur: this.currentUser, tweet: this.tweet.id}, responseType: 'text'}).then(response => {
        this.tweets = response.body
        this.loading = false
        this.$emit('retweeted', this.tweet.id)
      }, response => {
        console.log('error retweet')
      })
    }
  },
  props: ['tweet', 'currentUser'],
  created () {
    moment.locale('fr')
  }
}
</script>

<style scoped>
li.button {
 display: inline-block;
 cursor: pointer;
}

a {
 color: #42b983;
}

span.handle {
 color: gray;
}
</style>
