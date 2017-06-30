<template>
  <div class="utilisateurs">
      <select @change="onChange($event.target.value)">
       <option disabled value="">Choisissez un utilisateur ...</option>
       <option v-for="utilisateur in utilisateurs" :value="utilisateur.handle">
         {{ utilisateur.prenom }} {{ utilisateur.nom }}
       </option>
      </select>
  </div>
</template>

<script>
export default {
  name: 'timeline',
  data () {
    return {
      utilisateurs: []
    }
  },
  created () {
    this.getUtilisateurs()
  },
  methods: {
    onChange: function (handle) {
      this.$emit('changeUtilisateur', handle)
    },
    getUtilisateurs: function () {
      this.$http.get('http://localhost:8080/utilisateurs').then(response => {
        this.utilisateurs = response.body
      }, response => {
        console.log('error utilisateurs')
      })
    }
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
