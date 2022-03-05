<script setup>
import { computed } from 'vue';

const props = defineProps({
    heatPercentage: {
        type: Number
    },
    drillHeight: {
        type: Number
    }
});

const heatPercentageComputed = computed(() => {
    const val = props.heatPercentage;

    if(val > 100) return 100;
    else if(val < 0) return 0;

    return Number(val);
})

const style = computed(
    () => ({
        background: `linear-gradient(90deg, rgba(0,0,0,0) ${100 - heatPercentageComputed.value}%, rgba(255,59,0,0.4) 100%)`,
    })
);
</script>

<template>
    <div class="drill-image-container">
        <div class="drill-image-mask" :style="style"></div>
        <img src="src/assets/drill.png" :height="drillHeight" class="drill-image" />
    </div>
</template>

<style lang="scss">
    .drill-image-mask {
        -webkit-mask: url(src/assets/drill.png) center/contain no-repeat;
        position: absolute;
        width: 100%;
        height: 100%;
    }

    .drill-image-container {
        position: relative;
    }

    .drill-image {
        display: block;
    }
</style>