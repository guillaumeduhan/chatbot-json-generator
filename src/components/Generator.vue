<template lang="pug">
  #Generator
    h2 Create a new question
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
      b-form-radio(name="next-radio", v-model="question.next", value="false") Yes, my question has answers
      b-form-radio(name="next-radio", v-model="question.next", value="true") No, my question has no answer, switch to new one
</template>

<script>
export default {
  name: 'Generator',
  data() {
    return {
      question: {
        title: undefined,
        delay: 0,
        answers: {},
        next: false
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
