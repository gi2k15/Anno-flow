<style scoped>
.container {
    display: flex;
    justify-content: space-around;
    gap: 10px;
}

.industry-container {
    display: flex;
    flex-direction: column;
}

.radio-container {
    display: inline-flex;
    gap: 10px;
}
</style>

<template>
    <div class="container">
        <div class="industry-container">
            <label for="industry-name">Industry</label>
            <input type="text" id="industry-name" placeholder="Farm, Mine..." v-model="industryName">
        </div>
        <div class="industry-container">
            <label>Time (seconds)</label>
            <div class="radio-container">
                <label>
                    <input type="radio" name="time" class="time-radio" id="30" value="30" v-model="time">
                    30
                </label>
                <label>
                    <input type="radio" name="time" class="time-radio" id="60" value="60" v-model="time">
                    60
                </label>
                <label>
                    <input type="radio" name="time" class="time-radio" id="90" value="90" v-model="time">
                    90
                </label>
                <label>
                    <input type="radio" name="time" class="time-radio" id="120" value="120" v-model="time">
                    120
                </label>
                <input type="number" id="time-custom" placeholder="Custom time" v-model="time">
            </div>
        </div>
        <input type="button" value="Remove" @click="emit('remove')">
    </div>
</template>

<script setup>
const industryName = defineModel('industryName')
const time = defineModel('time')
const emit = defineEmits(['remove'])
</script>
