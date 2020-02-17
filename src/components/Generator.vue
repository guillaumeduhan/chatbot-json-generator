<template lang="pug">
  #Generator
    h2 Create a new question
    .line.title
      h5 Question number:
      b-input(placeholder="001", v-model="question.number")
    .line.title
      h5 Question title:
      b-input(placeholder="What is your favorite desert?", v-model="question.title")
    .line.range
      h5(for="range-1") Delay to appear:
      .d-flex.flex-row
        b-form-input(type="range", min="0", max="10", v-model="question.delay")
        .delay {{ question.delay }} secs.
    .line.next
      h5(for="range-1") Does my question has answers?
      b-form-radio(name="next-radio", v-model="question.next", value="true") Yes, my question has answers
      b-form-radio(name="next-radio", v-model="question.next", value="false") No, my question has no answer, go to next
    .line.answers--buttons(v-if="question.next === 'true'")
      h5 Add your answers
      AnswerGenerator(@answerSend="pushAnswerToAnswers")
</template>

<script>
import AnswerGenerator from './AnswerGenerator.vue'

export default {
  name: 'Generator',
  components: {
    AnswerGenerator
  },
  data() {
    return {
      question: {
        number: undefined,
        title: undefined,
        delay: 2,
        answers: undefined,
        next: 'true'
      }
    }
  },
  methods: {
    pushAnswerToAnswers(answer) {
      let size;
      if (this.question.answers) {
        size = Object.keys(this.question.answers).length;
        size = size + 1
        this.question.answers[size] = answer
      } else {
        size = 1
        this.question.answers = {
          [size]: answer
        }
      }
    }
  }
}
</script>

<style lang="scss" scoped>
#Generator {
  width: 100%;
  padding: 15px;
  border-radius: 5px;
  border: 1px solid #ddd;
  margin-bottom: 15px;
  max-width: 600px;

  .line {
    margin: 25px 0;

    &.range {
      .d-flex {
        .delay {
          min-width: 100px;
          margin: 0 20px;
        }
      }
    }
  }
}
</style>
