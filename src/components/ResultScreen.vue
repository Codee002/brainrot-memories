<template>
  <div class="screen d-flex justify-content-center flex-column align-items-center">
      <h1>Congratulations</h1>
      <h3>{{ Math.round(timePlay / 1000) }}seconds</h3>
      <button @click="onPlayAgain" >Play Again</button>
    </div>
</template>

<script>
export default {
  props:{
    timePlay: {
      type: [Number],
      required: true,
    }
  },


  methods: {
    onPlayAgain()
    {
      this.$emit("onPlayAgain");
    }
  },
}
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

button {
  font-size: 1.4rem;
  width: 9rem;
  padding: 2rem;
  border: 0.004rem solid var(--light);
  border-radius: 1rem;
  margin: 1rem;
  background-color: var(--dark);
  color: var(--light);
}

button:hover {
  background-color: var(--light);
  color: var(--dark);
  border: 0.004rem solid var(--dark);
}
</style>
