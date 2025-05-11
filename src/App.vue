<template>
  <main-screen v-if="statusMatch == 'default'" @onStart="onHandleBeforeStart" />
  <interac-screen v-if="statusMatch == 'match'" 
  :cards = "settings.cards" />
  <result-screen v-if="statusMatch == 'result'" />
  <footer-screen />
</template>

<script>
import MainScreen from "./components/MainScreen.vue";
import InteracScreen from "./components/InteracScreen.vue";
import ResultScreen from "./components/ResultScreen.vue";
import FooterScreen from "./components/FooterScreen.vue";

import { shuffled } from "./utils/array.js";

export default {
  name: "App",
  components: {
    MainScreen,
    InteracScreen,
    ResultScreen,
    FooterScreen,
  },

  data() {
    return {
      settings: {
        mode: 0,
        startAt: null,
        cards: [],
      },
      statusMatch: "default",
    };
  },

  methods: {
    onHandleBeforeStart(mode) {
      this.settings.mode = mode;

      // Tạo mảng, trộn KQ
      const firstCards = Array.from(
        { length: this.settings.mode / 2 },
        (_, i) => i + 1
      );
      const secondCards = [...firstCards];
      const cards = [...firstCards, ...secondCards];
      this.settings.cards = shuffled(shuffled(shuffled(shuffled(cards))));

      // Tạo thời gian chơi
      this.startAt = new Date().getTime();

      // Đổi giao diện
      this.statusMatch = "match";

    },
  },
};
</script>

<style>
</style>
