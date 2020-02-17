<template lang="pug">
  #AnswerGenerator
    .line.answers--list
      p(v-for="(ans, index) in answers", :key="index") {{ ans.title }}
    .line-input-answer
      b-input(placeholder="Your first answer here", v-model="answer.title")
      .line-link-to.d-flex.align-items-center.justify-content-start
        p This answer links to question number:
        b-input#answerNumberInput(placeholder="002", v-model="answer.linkTo")
    ErrorMessage(v-if="error", :title="error")
    b-button(variant="outline-primary", @click="pushAnswerToArray") Add your answer
</template>

<script>
import ErrorMessage from './ErrorMessage.vue'

export default {
  name: 'AnswerGenerator',
  components: {
    ErrorMessage
  },
  data() {
    return {
      answers: [],
      answer: {
        title: "Hey",
        type: 'answer',
        linkTo: "001"
      },
      error: undefined
    }
  },
  methods: {
    displayError(message) {
      this.error = message
      setTimeout(() => {
        this.error = undefined
      }, 3000)
    },
    pushAnswerToArray() {
      if (!this.answer.title) {
        this.displayError('Complete your an answer title, please.')
      } else if (this.answer.title.length > 500) {
        this.displayError('Answer title too long. Please shorten.')
      } else if (!this.answer.linkTo) {
        this.displayError('Please specify a valid link to a question.')
      } else {
        this.$emit('answerSend', this.answer)
      }
    }
  }
}
</script>

<style lang="scss" scoped>
#AnswerGenerator {
  padding: 15px;
  border: 1px solid #eee;

  p {
    margin: 0;
  }

  .line-input-answer {
    .line-link-to {
      margin-top: 5px;
    }
    #answerNumberInput {
      max-width: 50px;
      margin: auto 20px;
    }
  }
}
</style>
