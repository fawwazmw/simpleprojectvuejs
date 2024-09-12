<template>
  <div id="app">
    <h1 class="fun-text">Have Funnn mwwhwhwhwh</h1>
    <ClickCounter />
    <BoxColorChanger @colorChanged="updateBackgroundColor" />
    <ImageCarousel />
  </div>
</template>

<script>
import ClickCounter from "./components/ClickCounter.vue";
import BoxColorChanger from "./components/BoxColorChanger.vue";
import ImageCarousel from "./components/ImageCarousel.vue";

export default {
  components: {
    ClickCounter,
    BoxColorChanger,
    ImageCarousel,
  },
  methods: {
    updateBackgroundColor(newColor) {
      document.body.style.backgroundColor = newColor;
    },
  },
};
</script>

<style>
/* Styling for the main app */
#app {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  text-align: center;
  color: #2c3e50;
}

/* Styling for the Have Fun text */
.fun-text {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  font-size: 2.5rem;
  color: #ff5733; /* Fun orange color */
  margin-bottom: 20px;
}

/* Global reset for margins and paddings */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
</style>
