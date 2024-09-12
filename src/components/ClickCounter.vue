<template>
  <div class="click-counter">
    <h3>Click Counter</h3>
    <button @click="incrementCount" class="counter-button">Click me!</button>
    <p class="count-display">
      You clicked: <strong>{{ count }}</strong> times
    </p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      count: 0,
    };
  },
  methods: {
    incrementCount() {
      this.count++;
    },
  },
};
</script>

<style scoped>
.click-counter {
  text-align: center;
  margin: 20px auto;
  padding: 20px;
  max-width: 400px;
  background-color: #f9fafc;
  border-radius: 10px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
}

h3 {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  font-size: 1.5rem;
  color: #333;
  margin-bottom: 15px;
}

.counter-button {
  padding: 12px 25px;
  background-color: #3498db;
  color: white;
  font-size: 1rem;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s ease, transform 0.2s ease;
}

.counter-button:hover {
  background-color: #2980b9;
  transform: scale(1.05);
}

.count-display {
  margin-top: 15px;
  font-size: 1.2rem;
  color: #333;
}
</style>
