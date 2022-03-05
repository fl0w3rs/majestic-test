<script setup>
import { computed, ref } from 'vue';
import Drill from './DrillComponents/Drill.vue';
import Latch from './DrillComponents/Latch.vue';
import Spring from './DrillComponents/Spring.vue';

const heatPctg = ref(0);
const movePercentage = ref(0);

const movePercentageComputed = computed(() => {
  if(movePercentage.value > 100) return 100;
  if(movePercentage.value < 0) return 0;
  return movePercentage.value;
})

const drillStyle = computed(() => ({
  left: `-${140 - (movePercentageComputed.value / 100 * 75)}%`,
  transitionDuration: '.5s',
}))

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
    Процент продвижения: {{movePercentageComputed}} <input v-model="movePercentage" type="number" min="0" max="100" placeholder="move percentage" /><br/>
    <button @click="startSimulation">Симулировать движение с нагревом</button>
    


    <div style="overflow: hidden" class="working-round position-relative d-flex row flex-center-xy">
      <drill class="position-absolute" style="z-index: 1" :heatPercentage='heatPctg' :style="drillStyle" />
      <div class="position-absolute d-flex row flex-center-xy hw-100">
        <div v-for="index in 5" class="key-column">
          <div class="align-center d-flex column key-column-bg" style="height: 50%; justify-content: flex-end">
            <spring :progress="movePercentageComputed" />
            <latch :onTop="true" :progress="movePercentageComputed" />
          </div>
          <div class="align-center column" style="background-color: #7B7B7B; display: flex; justify-content: flex-start">
            <latch :onTop="false" :progress="movePercentageComputed" />
          </div>
        </div>
      </div>
      <div class="position-absolute d-flex" style="align-items: flex-end; height: 100%; width: 100%">
        <div class="d-flex column" style="background-color: #8f8f8f; height: 20%; width: 100%">
          <div class="height: 30%; width: 100%; background-color: #eeeeee;">
gg
          </div>
          <div class="height: 70%; width: 100%">
hh
          </div>
        </div>
      </div>
    </div>
  </div>
  
</template>

<style lang="scss">
  .main-page {
    background-color: #121212;
    height: 100%;
  }

  .working-round {
    width: 450px;
    height: 450px;
    background-color: #1C1D1E;
    border-radius: 100%;
  }

  .d-flex {
    display: flex;
  }

  .spring {
    z-index: 1;
    height: 70%;
    width: 60%; 
  }

  .key-column {
    height: 100%;
    width: 40px;
    margin: auto 2%;
  }

  .key-column-bg {
    background-color: #7B7B7B;
  }

  .hw-100 {
    height: 100%;
    width: 100%;
  }

  .row {
    flex-direction: row;
  }

  .column {
    flex-direction: column;
  }

  .align-center {
    align-items: center;
  }

  .justify-center {
    justify-content: center;
  }

  .flex-center-xy {
    align-items: center;
    justify-content: center;
  }

</style>