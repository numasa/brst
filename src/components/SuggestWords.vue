<template>
  <v-container fluid>
    <v-row>
      <v-col cols="12">
        <v-text-field
          v-model="searchText"
          ref="text"
          :label="label"
          :outlined="outlined"
          :rounded="rounded"
        ></v-text-field>
      </v-col>
    </v-row>
    <v-row>
      <v-col cols="12">
        <v-layout justify-center>
          <v-btn
            large
            color="primary"
            @click="startSuggest($refs.text.value)"
          >start</v-btn>
        </v-layout>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import axios from "axios";
const URL = 'URL_FOR_SUGGEST_API'

export default {
  data() {
    return {
      searchText: '',
      label: '検索文字',
      outlined: true,
      rounded: true,
      word: this.$props.searchword,
    }
  },
  props: [
    'searchword',
  ],
  methods: {
    startSuggest(word) {
      if (word) {
        axios.get(URL + word)
        .then(response => {
          this.$emit('set', response.data)
        })
      }
    }
  },
  watch: {
    searchword: function (newVal) {
      axios.get(URL + newVal)
      .then(response => {
        this.$emit('set', response.data)
      })
    }
  }
}
</script>

<style>
</style>
