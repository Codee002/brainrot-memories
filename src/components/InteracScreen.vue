<template>
  <div class="screen">
    <div :style="gridStyle" class="card-grid">
      <card-flip
        v-for="(card, index) in cards"
        :key="index"
        :imgUrl="getImageUrl(card, index)"
        :soundUrl="getSoundUrl(card)"
        :ref="`card-${index}`"
        :card="{ index, value: card }"
        @onFlip="checkRule($event)"
      />
    </div>
  </div>
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

  data() {
    return {
      rules: [],
      column: Math.sqrt(this.cards.length),
    };
  },

  computed: {
    gridStyle() {
      return {
        display: "grid",
        "grid-template-columns": `repeat(${this.column}, 1fr)`,
        gap: "-1rem",
      };
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
    },

    getSoundUrl(card) {
      const url = `assets/brainrot/sounds/${card}.mp3`;
      return window.location.href + url;
    },

    checkRule(event) {
      if (this.rules.length >= 2) {
        // for (let key in this.rules)
        // {
        //   this.$refs[`card-${this.rules[key].index}`][0].flipBack();
        //   console.log("Tràn", this.$refs[`card-${this.rules[key].index}`][0])
        // }
        // this.rules = [];
        // return false;
      }
      this.rules.push(event);
      if (
        this.rules.length == 2 &&
        this.rules[0].value == this.rules[1].value
      ) {
        this.$refs[`card-${this.rules[0].index}`][0].muteSound();
        this.rules = [];
        const disableElements = document.querySelectorAll(
          ".card__inner.is-disable"
        );

        // Hoàn thành trò chơi
        if (disableElements.length == this.cards.length - 1) {
          setTimeout(() => {
            this.$emit("onFinish");
          }, 800);
        }
      } else if (
        this.rules.length == 2 &&
        this.rules[0].value != this.rules[1].value
      ) {
        setTimeout(() => {
          this.$refs[`card-${this.rules[0].index}`][0].flipBack();
          this.$refs[`card-${this.rules[1].index}`][0].flipBack();
          this.rules = [];
        }, 700);
      }
    },
  },
};
</script>

<style scopted>
.screen {
    width: 90%;
    height: 100%;
    margin: auto;
}

.screen__inner {
  /* display: flex;
  justify-content: center; */
}
.card-grid {
  width: 100%;
  /* max-width: 1200px; */
  margin: auto;
  /* padding: 16px; */
}
</style>
