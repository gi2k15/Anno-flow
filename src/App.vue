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
</style>

<template>
  <div class="main-containter">
    <h1>Anno 117 Flow Calculator</h1>
    <p>This app calculates how many of each build you need to construct based on the time
      each one takes to make a product, so the chain is fully optimized.
    </p>
    <input type="button" value="Add building" @click="addBuilding" style="height: 2rem;">
    <Building 
      v-for="(building, index) in listBuildings" 
      :key="index" 
      v-model:industry-name="building.name"
      v-model:time="building.time"
      @remove="removeBuilding(index)">
    </Building>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import Building from './Building.vue'

function addBuilding() {
  listBuildings.value.push({ ...buildingObject })
}

function removeBuilding(index) {
  listBuildings.value.splice(index, 1)
}

const buildingObject = {
  name: '',
  time: null,
}
const listBuildings = ref([])

addBuilding()
</script>
