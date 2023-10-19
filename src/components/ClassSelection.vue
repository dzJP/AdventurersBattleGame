<template>
	<div class="class-selection">
		<h1>Select Your Class</h1>
		<div v-for="className in classes" :key="className" class="class-container">
			<div class="class-name" v-if="selectedClass === className">{{ className }}</div>
			<img :src="getImageSource(className)" :alt="className"
				:class="{ 'class-image': true, 'selected': selectedClass === className }" @click="highlightImage(className)"
				@mouseover="hoveredClass = className" @mouseout="hoveredClass = null" />
		</div>
		<div v-if="selectedClass" class="faction-selection">
			<h2>Select Your Faction</h2>
			<div class="faction-tooltip">
				<img src="/faction-icons/Horde_Crest.png" alt="Horde" @click="selectFaction('Horde')"
					:class="{ 'selected': selectedFaction === 'Horde' }" />
				<img src="/faction-icons/Alliance_Crest.png" alt="Alliance" @click="selectFaction('Alliance')"
					:class="{ 'selected': selectedFaction === 'Alliance' }" />
			</div>
		</div>
		<div v-if="selectedFaction" class="race-selection">
			<h2>Select Your Race</h2>
			<div class="race-container">
				<div v-for="race in validRaces" :key="race" class="race-item">
					<img :src="getRaceImageSource(race)" :alt="race"
						:class="{ 'race-image': true, 'selected': selectedRace === race, 'invalid': !isValidCombination() }"
						@click="selectRace(race)" />
				</div>
			</div>
		</div>
		<div v-if="selectedClass && selectedFaction && selectedRace" class="result">
			<h2>Selected:</h2>
			<div class="selected-info">{{ selectedRace }} {{ selectedClass }} - {{ selectedFaction }}</div>
		</div>
		<div v-if="selectedClass && selectedFaction && selectedRace" class="character-name">
			<label for="characterName">Enter Character Name:</label>
			<input type="text" id="characterName" v-model="characterName" />
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
			selectedRace: null,
			hoveredClass: null,
			characterName: '',
			classes: ['Warrior', 'Mage', 'Paladin', 'Hunter', 'Druid'],
			factions: ['Horde', 'Alliance'],
			races: {
				Horde: ['Orc', 'Troll', 'Undead'],
				Alliance: ['Human', 'Dwarf', 'NightElf'],
			},
			classRaceRestrictions: {
				Mage: ['Orc', 'NightElf', 'Dwarf'],
				Paladin: ['Orc', 'Troll', 'Undead'],
				Hunter: ['Undead'],
				Druid: ['Undead', 'Human', 'Dwarf'],
			},
		};
	},
	methods: {
		highlightImage(className) {
			console.log('Selected class:', className);
			this.selectedClass = className;
			this.selectedFaction = null; // Reset selected faction
			this.selectedRace = null; // Reset selected race
		},
		getImageSource(className) {
			return `/class-icons/${className}_Crest.png`;
		},
		selectFaction(faction) {
			console.log('Selected faction:', faction);
			this.selectedFaction = faction;
			this.selectedRace = null; // Reset selected race
		},
		getRaceImageSource(race) {
			return `/race-icons/${this.selectedFaction}/${race}.png`;
		},
		selectRace(race) {
			console.log('Selected race:', race);
			this.selectedRace = race;
		},
		isValidCombination() {
			const selectedClass = this.selectedClass;
			const selectedRace = this.selectedRace;

			if (this.classRaceRestrictions[selectedClass]) {
				return !this.classRaceRestrictions[selectedClass].includes(selectedRace);
			}

			return true;
		},
	},
	computed: {
		validRaces() {
			const selectedClass = this.selectedClass;
			const selectedFaction = this.selectedFaction;

			if (selectedClass && selectedFaction) {
				return this.races[selectedFaction].filter(
					(race) =>
						!this.classRaceRestrictions[selectedClass] ||
						!this.classRaceRestrictions[selectedClass].includes(race)
				);
			}

			return [];
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

.character-name {
	margin-top: 20px;
}

.character-name label {
	font-size: 18px;
	font-weight: bold;
	color: #2c3e50;
}

.character-name input {
	font-size: 16px;
	padding: 8px;
	border: 2px solid #ccc;
	border-radius: 4px;
	margin-top: 8px;
}

.race-selection {
	text-align: center;
}

.race-container {
	display: flex;
	justify-content: center;
	margin-top: 10px;
}

.race-item {
	margin: 0 10px;
}

.race-image {
	width: 200px;
	height: 200px;
	object-fit: cover;
	border-radius: 50%;
	margin: 10px;
}

.race-image.selected {
	outline: 2px solid red;
}

.invalid {
	filter: grayscale(100%);
}
</style>