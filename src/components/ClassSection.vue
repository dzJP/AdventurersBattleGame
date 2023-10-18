<template>
    <div>
      <h1>Select Your Class</h1>
      <img
        src="@/assets/orc-warrior_847279-532.jpg"
        alt="Orc Warrior"
        @click="highlightImage"
        ref="image"
      />
    </div>
  </template>
  
  <script>
  export default {
    name: 'ClassSelection',
    methods: {
      highlightImage() {
        this.$refs.image.classList.toggle('highlighted-image');
      }
    }
  }
  </script>
  
  <style scoped>
  .highlighted-image {
    border: 2px solid red;
  }
  </style>
  