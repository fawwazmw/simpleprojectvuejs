<template>
  <div class="box-color-changer">
    <h3>Box Color Changer</h3>
    <div class="box" :style="{ backgroundColor: currentColor }"></div>
    <label for="color-picker" class="color-label">Pick a color:</label>
    <input
      id="color-picker"
      type="color"
      v-model="currentColor"
      @input="emitColorChange"
      class="color-picker"
    />
  </div>
</template>

<script>
export default {
  data() {
    return {
      currentColor: "#ff0000", // Default color
    };
  },
  methods: {
    emitColorChange() {
      this.$emit("colorChanged", this.currentColor); // Emit color change event
    },
  },
};
</script>

<style scoped>
/* BoxColorChanger styling */
.box-color-changer {
  text-align: center;
  margin: 20px;
}
.box {
  width: 150px;
  height: 150px;
  margin: 20px auto;
  border-radius: 10px;
  transition: background-color 0.5s ease;
  box-shadow: 0 8px 20px rgba(0, 0, 0, 0.15);
}
.color-label {
  display: block;
  margin-bottom: 10px;
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  font-size: 1rem;
  color: #555;
}
.color-picker {
  width: 60px;
  height: 60px;
  border: none;
  cursor: pointer;
  background: none;
  padding: 0;
  outline: none;
  transition: transform 0.3s ease;
}
.color-picker:hover {
  transform: scale(1.1);
}
.color-picker::-webkit-color-swatch {
  border-radius: 50%;
  border: 2px solid #ddd;
}
.color-picker::-webkit-color-swatch-wrapper {
  padding: 0;
}
</style>
