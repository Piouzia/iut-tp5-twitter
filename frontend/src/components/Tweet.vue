<template>
  <div class="tweet">
    {{ tweet.auteur }} dit : {{ tweet.contenu }}
  </div>
</template>

<script>
export default {
  name: 'tweet',
  props: ['tweet']
}
</script>
