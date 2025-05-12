<template>
  <div
    class="d-flex justify-content-center flex-column align-items-center screen"
  >
    <div class="d-flex justify-content-center flex-column align-items-center ">
      <h1>Brainrot Memories</h1>
      <h3>Select mode to start game</h3>
    </div>
    <div class="action">
      <button @click="onStart(16)">
        <span>4x4</span> <br>
        <span>Easy</span>
      </button>
      <button @click="onStart(36)">
        <span>6x6</span> <br>
        <span>Normal</span>
      </button>
      <button @click="onStart(64)">
        <span>8x8</span> <br>
        <span>Hard</span>
      </button>
    </div>
  </div>
</template>

<script>
export default {
  methods: {
    onStart(mode) {
      this.$emit("onStart", mode);
    },
  },
};
</script>

<style scoped>
.screen {
  margin-top: 9rem;
}

h1 {
  font-size: 4rem;
}

h3 {
  font-size: 2rem;
}

.action button {
  font-size: 1.4rem;
  width: 9rem;
  padding: 2rem;
  border: 0.004rem solid var(--light);
  border-radius: 1rem;
  margin: 1rem;
  background-color: var(--dark);
  transition: 0.3s;
  color: var(--light);
}

.action button:hover {
  background-color: var(--light);
  color: var(--dark);
  border: 0.004rem solid var(--dark);
}
</style>
