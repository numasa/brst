<template>
  <v-app>
    <v-app-bar app>
      <v-toolbar-title class="headline text-uppercase">
        <span>Brain Storming Support</span>
      </v-toolbar-title>
      <v-toolbar-items class="col-9">
        <Theme />
      </v-toolbar-items>
      <v-spacer></v-spacer>
    </v-app-bar>

    <v-content>
      <v-tabs
        background-color="deep-purple accent-4"
        dark
      >
        <v-tabs-slider></v-tabs-slider>
        <v-tab>アイデア整理</v-tab>
        <v-tab-item>
          <IdeaInput @set="setInput"/>
          <div v-if="ideas.length">
            <IdeaItems :ideas="ideas" />
          </div>
          <div v-else></div>
        </v-tab-item>

        <v-tab>関連文字検索</v-tab>
        <v-tab-item>
          <SuggestWords @set="setData" :searchword="searchword"/>
          <SuggestItems @set="setWord" :keyword="suggestResult"/>
        </v-tab-item>
      </v-tabs>
    </v-content>
  </v-app>
</template>

<script>
import Theme from './components/Theme';
import IdeaInput from './components/IdeaInput';
import IdeaItems from './components/IdeaItems';
import SuggestItems from './components/SuggestItems';
import SuggestWords from './components/SuggestWords';

export default {
  name: 'App',
  components: {
    Theme,
    IdeaInput,
    IdeaItems,
    SuggestItems,
    SuggestWords,
  },
  data: function () {
    return {
      suggestResult: [],
      ideas: [],
      searchword: '',
    }
  },
  methods: {
    setInput(data) {
      this.$data.ideas.push(data);
    },
    setData(data) {
      this.$data.suggestResult = data
    },
    setWord(data) {
      this.$data.searchword = data
    }
  },
};
</script>
