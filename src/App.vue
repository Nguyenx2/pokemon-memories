<template>
  <div>
    <main-screen
      v-if="statusMatch === 'default'"
      @onStart="onHandleBeforeStart($event)"
    />
    <interact-screen
      v-if="statusMatch === 'match'"
      :cardsContext="settings.cardsContext"
    />
  </div>
</template>

<script>
import InteractScreen from "./components/InteractScreen.vue";
import MainScreen from "./components/MainScreen.vue";

import { shuffled } from "./utils/array";

export default {
  name: "App",
  data() {
    return {
      settings: {
        totalOfBlocks: 0,
        cardsContext: [],
        startedAt: null,
      },
      statusMatch: "default",
    };
  },
  components: {
    MainScreen,
    InteractScreen,
  },
  methods: {
    onHandleBeforeStart(config) {
      console.log("running handle ...", config);
      this.settings.totalOfBlocks = config.totalOfBlocks;

      const firstCards = Array.from(
        { length: this.settings.totalOfBlocks / 2 },
        (_, i) => i + 1
      );
      const seccondCards = [...firstCards];
      const cards = [...firstCards, ...seccondCards];
      this.settings.cardsContext = shuffled(
        shuffled(shuffled(shuffled(cards)))
      );

      this.settings.startedAt = new Date().getTime();
      console.log(this.settings.cardsContext);
      this.statusMatch = "match";
    },
  },
};
</script>
