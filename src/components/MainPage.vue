<script setup>
import { ref } from 'vue';
import DrillCircle from './DrillCircle.vue';

const heatPctg = ref(0);
const movePercentage = ref(0);

const startSimulation = () => {
  const interval = setInterval(() => {
    movePercentage.value += 1;
    heatPctg.value += Math.random();

    if(movePercentage.value >= 100) clearInterval(interval);
  }, 100)
}

</script>

<template>
  <div class="d-flex column flex-center-xy main-page">
    Процент нагрева: {{heatPctg}}. <input v-model="heatPctg" type="number" min="0" max="100" placeholder="heat percentage" /><br/>
    Процент продвижения: {{movePercentage}} <input v-model="movePercentage" type="number" min="0" max="100" placeholder="move percentage" /><br/>
    <button @click="startSimulation">Симулировать движение с нагревом</button>
    

    <drill-circle :heatPctg="heatPctg" :movePercentage="movePercentage" />
    
  </div>
  
</template>

<style lang="scss">
  .main-page {
    background-color: #121212;
    height: 100%;
  }

</style>