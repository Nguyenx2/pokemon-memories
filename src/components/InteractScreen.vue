<template>
  <div>
    <div class="scre">
      <h1>Interact Components here ...</h1>
      <card-flip
        v-for="(card, index) in cardsContext"
        :key="index"
        :imgBackFaceUrl="`images/${card}.png`"
      />
    </div>
  </div>
</template>
<script>
import CardFlip from "./CardGame.vue";
export default {
  props: {
    cardsContext: {
      type: Array,
      default: function () {
        return [];
      },
    },
  },
  components: {
    CardFlip,
  },
};
</script>
