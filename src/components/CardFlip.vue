<template>
  <div class="card">
    <div
      class="card__inner"
      @click="flipCard"
      :class="{ 'is-flipped': isFlip }"
    >
      <div class="card__face card__face--front">
        <div
          class="card__content"
          :style="{ backgroundImage: `url(${image})` }"
        ></div>
      </div>
      <div class="card__face card__face--back">
        <div class="card__content"></div>
      </div>
      <audio ref="clickSound" :src="soundUrl" preload="auto"></audio>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    imgUrl: {
      type: Promise,
      required: true,
    },

    soundUrl: {
      type: String,
      required: true,
    },
  },

  data() {
    return {
      isFlip: false,
      isMute: false,
      image: "",
    };
  },

  methods: {
    flipCard() {
      this.isFlip = !this.isFlip;

      this.$refs.clickSound.muted = this.isMute;
      this.isMute = !this.isMute;
      this.$refs.clickSound.currentTime = 0;
      this.$refs.clickSound.play();

      this.imgUrl.then((url) => {
        this.image = url;
      });
    },
  },
};
</script>

<style lang="css" scoped>
.card {
  display: inline-flex;
  width: 7.5rem;
  height: 10rem;
  margin: 1rem;
  border-radius: 1rem;
  border: 0px;
  color: var(--dark);
}

.card__inner {
  position: relative;
  cursor: pointer;
  width: 100%;
  height: 100%;
  transition: 1s;
  transform-style: preserve-3d;
  background-color: var(--light);
}

.card__inner.is-flipped {
  transform: rotateY(-180deg);
}

.card__face {
  position: absolute;
  width: 100%;
  height: 100%;
  backface-visibility: hidden;
  overflow: hidden;
  border-radius: 1rem;
  padding: 0rem;
  box-shadow: 0 3px 10px 3px rgba(0, 0, 0, 0.2);
}

.card__face--front {
  transform: rotateY(-180deg);
}

.card__face--front .card__content {
  background-size: cover;
  height: 100%;
  width: 100%;
  background-repeat: no-repeat;
  background-position: center;
}

.card__face--back .card__content {
  background: url("../../public/assets/brainrot/images/icon-back.png") no-repeat
    center center;
  background-size: cover;
  height: 100%;
  width: 100%;
}
</style>
