<template>
    <div class="class-selection">
      <h1>Select Your Class</h1>
      <div class="class-container" @click="highlightImage('Warrior')">
        <img
          src="/class-icons/Warrior_Crest.png"
          alt="Warrior"
          class="class-image"
        />
      </div>
      <div class="class-container" @click="highlightImage('Mage')">
        <img
          src="/class-icons/Mage_Crest.png"
          alt="Mage"
          class="class-image"
        />
      </div>
      <div class="class-container" @click="highlightImage('Paladin')">
        <img
          src="/class-icons/Paladin_Crest.png"
          alt="Paladin"
          class="class-image"
        />
      </div>
      <div class="class-container" @click="highlightImage('Hunter')">
        <img
          src="/class-icons/Hunter_Crest.png"
          alt="Hunter"
          class="class-image"
        />
      </div>
      <div class="class-container" @click="highlightImage('Druid')">
        <img
          src="/class-icons/Druid_Crest.png"
          alt="Druid"
          class="class-image"
        />
      </div>
    </div>
  </template>
  
  <script>
  export default {
    name: 'ClassSelection',
    methods: {
      highlightImage(className) {
        console.log('Selected class:', className);
      }
    }
  }
  </script>
  
  <style scoped>
  .class-selection {
    text-align: center;
  }
  
  .class-container {
    display: inline-block;
    margin: 20px;
    cursor: pointer;
  }
  
  .class-image {
    max-width: 150px; /* Adjust as needed */
  }
  </style>
  