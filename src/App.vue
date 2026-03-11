<style>
body {
  background-color: rgb(19, 19, 19);
  font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
  color: white;
}
</style>

<style scoped>
.main-containter {
  margin: 0 auto;
  width: 80%;
  display: flex;
  flex-direction: column;
  gap: 10px;
}

input {
  height: 3rem;
  font-size: larger;
}
</style>

<template>
  <div class="main-containter">
    <h1>Anno 117 Flow Calculator</h1>
    <p>This app calculates how many of each build you need to construct based on the time
      each one takes to make a product, so the chain is fully optimized.
    </p>
    <input type="button" value="Add building" @click="addBuilding">
    <Building 
      v-for="(building, index) in listBuildings" 
      :key="index" 
      v-model:industry-name="building.name"
      v-model:time="building.time"
      @remove="removeBuilding(index)">
    </Building>

    <div class="result-box">
      <h2>Optimized Flow</h2>
      <p v-if="optimizedBuildings.length === 0">
        Fill in valid production times to calculate.
      </p>
      <ul v-else>
        <li v-for="item in optimizedBuildings" :key="item.id">
          {{ item.name }}: {{ item.required }} {{ item.required < 2 ? "building" : "buildings" }}
        </li>
      </ul>
    </div>
    <input type="button" value="Reset" @click="resetBuildings">
  </div>
</template>

<script setup>
import { computed, ref } from 'vue'
import Building from './Building.vue'

function addBuilding() {
  listBuildings.value.push({ ...buildingObject })
}

function removeBuilding(index) {
  listBuildings.value.splice(index, 1)
}

function resetBuildings() {
  listBuildings.value.length = 0
  addBuilding()
}

function gcd(a, b) {
  let x = Math.abs(a)
  let y = Math.abs(b)
  while (y !== 0) {
    const temp = y
    y = x % y
    x = temp
  }
  return x || 1
}

function gcdArray(values) {
  return values.reduce((acc, value) => gcd(acc, value))
}

function isNaturalNumber(value) {
  return Number.isInteger(value) && value > 0
}

function calculateOptimizedBuildings(buildings) {
  const normalized = buildings
    .map((building, index) => {
      const time = Number(building.time)
      return {
        id: `${index}-${building.name || 'building'}`,
        name: building.name?.trim() || `Building ${index + 1}`,
        time
      }
    })
    .filter((building) => isNaturalNumber(building.time))

  if (normalized.length === 0) return []

  const times = normalized.map((building) => building.time)
  const ratioGcd = gcdArray(times)

  return normalized.map((building, index) => ({
    ...building,
    required: times[index] / ratioGcd
  }))
}

const optimizedBuildings = computed(() => calculateOptimizedBuildings(listBuildings.value))

const buildingObject = {
  name: '',
  time: '',
}
const listBuildings = ref([])

const numInitialBuildings = 2
for(let i = 0; i < numInitialBuildings; i++) {
  addBuilding()
}
</script>
