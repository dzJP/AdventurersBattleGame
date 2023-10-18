<template>
  <div class="class-selection">
    <h1>Select Your Class</h1>
    <div v-for="className in classes" :key="className" class="class-container">
      <div class="class-name" v-if="selectedClass === className">{{ className }}</div>
      <img 
        :src="getImageSource(className)" 
        :alt="className"
        :class="{ 'class-image': true, 'selected': selectedClass === className }" 
        @click="highlightImage(className)"
        @mouseover="hoveredClass = className" 
        @mouseout="hoveredClass = null" 
      />
    </div>
    <div v-if="selectedClass" class="faction-selection">
      <h2>Select Your Faction</h2>
      <div class="faction-tooltip">
        <img 
          src="/faction-icons/Horde_Crest.png" 
          alt="Horde" 
          @click="selectFaction('Horde')" 
          :class="{ 'selected': selectedFaction === 'Horde' }" 
        />
        <img 
          src="/faction-icons/Alliance_Crest.png" 
          alt="Alliance" 
          @click="selectFaction('Alliance')" 
          :class="{ 'selected': selectedFaction === 'Alliance' }" 
        />
      </div>
    </div>
    <div v-if="selectedClass && selectedFaction" class="result">
      <h2>Selected:</h2>
      <div class="selected-info">{{ selectedClass }} {{ selectedFaction }}</div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ClassSelection',
  data() {
    return {
      selectedFaction: null,
      selectedClass: null,
      hoveredClass: null,
      classes: ['Warrior', 'Mage', 'Paladin', 'Hunter', 'Druid'],
    };
  },
  methods: {
    highlightImage(className) {
      console.log('Selected class:', className);
      this.selectedClass = className;
      this.selectedFaction = null; // Reset selected faction
    },
    getImageSource(className) {
      return `/class-icons/${className}_Crest.png`;
    },
    selectFaction(faction) {
      console.log('Selected faction:', faction);
      this.selectedFaction = faction;
    },
  },
};
</script>

<style scoped>
  .class-selection {
    text-align: center;
  }

  .class-container {
    display: inline-block;
    margin: 20px;
    cursor: pointer;
    position: relative;
  }

  .class-image {
    max-width: 150px;
  }

  .selected {
    outline: 2px solid red;
  }

  .class-name {
    position: absolute;
    bottom: -35px;
    right: 50%;
    transform: translateX(50%);
    font-size: 18px;
    font-weight: bold;
    color: #2c3e50;
  }

  .faction-selection {
    text-align: center;
  }

  .faction-tooltip {
    display: flex;
    justify-content: center;
    margin-top: 10px;
  }

  .faction-tooltip img {
    max-width: 150px;
    cursor: pointer;
    margin: 0 5px;
    border: 2px solid transparent;
  }

  .faction-tooltip img.selected {
    border-color: red;
  }

  .result {
    margin-top: 20px;
  }

  .selected-info {
    font-size: 24px;
    font-weight: bold;
    color: #2c3e50;
  }
</style>
