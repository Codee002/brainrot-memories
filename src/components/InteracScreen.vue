<template>
  <h1>InteracScreen</h1>
  <card-flip
    v-for="(card, index) in cards"
    :key="index"
    :imgUrl="getImageUrl(card, index)"
    :soundUrl="getSoundUrl(card)"
  />
</template>

<script>
import CardFlip from "./CardFlip.vue";

export default {
  props: {
    cards: {
      type: Array,
      default: function () {
        return [];
      },
    },
  },

  components: {
    CardFlip,
  },

  methods: {
    async getImageUrl(card) {
      const extensions = ["jpg", "webp", "png"];
      for (let ext of extensions) {
        const url = `assets/brainrot/images/${card}.${ext}`;
        console.log(url);
        try {
          const res = await fetch(url);
          if (res.ok) {
            return window.location.href + url;
          } else if (res.status === 404) {
            console.log(`Không tìm thấy: ${url}, thử đuôi khác.`);
            continue;
          }
        } catch (e) {
          console.error("Lỗi khi kiểm tra file:", e);
          return false;
        }
        return null;
      }
      // console.log(card, index);
    },

    getSoundUrl(card) {
      const url = `assets/brainrot/sounds/${card}.mp3`;
      // console.log(window.location.href + url, card)
      return window.location.href + url;
    },
  },
};
</script>
