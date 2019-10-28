<template>
  <v-container fluid>
    <v-row>
      <v-col cols="12">
        <v-text-field
          v-model="inputText"
          ref="idea"
          :label="label"
          :outlined="outlined"
          :rounded="rounded"
          :clearable="clearable"
        ></v-text-field>
      </v-col>
    </v-row>
    <v-row>
      <v-col cols="12">
        <v-layout justify-center>
          <v-btn
            large
            color="primary"
            @click="startIdeaInput($refs.idea.value)"
          >登録</v-btn>
        </v-layout>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  data() {
    return {
      inputText: '',
      label: 'アイデア入力',
      outlined: true,
      rounded: true,
      clearable: true,
    }
  },
  methods: {
    startIdeaInput(input) {
      this.$emit('set', input)
    }
  },
}
</script>

<style>
</style>
