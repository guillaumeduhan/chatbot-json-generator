<template lang="pug">
#Home
  header
    h1 Welcome to chatbot-generator
    p Create all your questions and answers for your chatbot. Get a JSON back.
  .content
    Generator(v-if="open")
    b-button(variant="outline-primary", @click="openGenerator") Create a question
  .model {{model}}
</template>

<script>
import Generator from '../components/Generator.vue'

export default {
  name: 'Home',
  components: {
    Generator
  },
  methods: {
    openGenerator() {
      this.open = true
    }
  },
  data() {
    return {
      open: false,
      model: {
        data: {

        }
      }
    }
  }
}
</script>

<style lang="scss">
#Home {
  text-align: left;

  header {
    margin: 20px 0;
  }

  img {
    max-width: 400px;
  }
}
</style>
