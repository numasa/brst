<template>
  <v-text-field
    v-model="inputText"
    ref="idea"
    :label="label"
    :outlined="outlined"
    :rounded="rounded"
    :clearable="clearable"
  ></v-text-field>
</template>

<script>
export default {
  data() {
    return {
      inputText: '',
      label: 'テーマ',
      outlined: false,
      rounded: false,
      full_width: false,
      clearable: true,
    }
  },
}
</script>

<style>
</style>
