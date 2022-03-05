<script setup>
import { computed } from 'vue';
import Drill from './DrillComponents/Drill.vue';
import Latch from './DrillComponents/Latch.vue';
import Spring from './DrillComponents/Spring.vue';

const props = defineProps({
    heatPctg: {
        type: Number
    },
    movePercentage: {
        type: Number
    },
    width: {
        type: Number,
        default: 300,
    },
    height: {
        type: Number,
        default: 300,
    }
})



const movePercentageComputed = computed(() => {
  if(props.movePercentage > 100) return 100;
  if(props.movePercentage < 0) return 0;
  return props.movePercentage;
})

const drillStyle = computed(() => ({
  left: `-${140 - (movePercentageComputed.value / 100 * 80)}%`,
  transitionDuration: '.5s',
}))

</script>

<template>
    <div style="overflow: hidden" class="working-round position-relative d-flex row flex-center-xy" :style="{ width: `${width}px`, height: `${height}px` }">

      <drill class="position-absolute" style="z-index: 1" :drillHeight="height * 0.11" :heatPercentage='heatPctg' :style="drillStyle" />
      <div class="position-absolute d-flex row flex-center-xy hw-100">
        <div v-for="index in 5" class="key-column" :style='{ width: (0.09 * width) + "px" }'>
          <div class="align-center d-flex column key-column-bg" style="height: 50%; justify-content: flex-end">
            <spring :progress="movePercentageComputed" :width="0.08 * width" />
            <latch :onTop="true" :progress="movePercentageComputed" :width="0.08 * width" />
          </div>
          <div class="align-center column key-column-bg" style="display: flex; justify-content: flex-start">
            <latch :onTop="false" :progress="movePercentageComputed" :width="0.08 * width" />
          </div>
        </div>
      </div>
      <div class="position-absolute d-flex" style="align-items: flex-end; height: 100%; width: 100%">
        <div class="d-flex column" style="background-color: #8f8f8f; height: 20%; width: 100%">
        </div>
      </div>
    </div>
</template>

<style lang="scss">
  .working-round {
    background-color: #1C1D1E;
    border-radius: 100%;
  }

  .key-column {
    height: 100%;
    margin: auto 2%;
  }

  .key-column-bg {
    background-color: #7B7B7B;
  }
</style>