<template lang="pug">
  #ErrorMessage
    p.text-danger {{ title }}
</template>

<script>
export default {
  name: 'ErrorMessage',
  props: {
    title: String
  }
}
</script>

<style lang="scss" scoped>
#ErrorMessage {

}
</style>
