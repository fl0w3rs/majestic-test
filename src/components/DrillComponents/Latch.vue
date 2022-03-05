<script setup>
import { computed } from 'vue';
import { getRandomNumberBetween } from '../../utils';

const props = defineProps({
    onTop: Boolean,
    progress: Number,
    width: Number
})

const random = getRandomNumberBetween(-2, 2);

const progress = computed(() => props.progress / 100)
const sign = computed(() => props.onTop ? -1 : 1);

const style = computed(() => {
    const rotateAngle = (props.onTop ? 0 : 180) + (progress.value * (3 + random) * sign.value);

    const style = {
        transform: `rotate(${rotateAngle}deg)`
    }

    if(props.onTop) {
        style.transform = `translate(0px, ${progress.value * 15 * -1}px) ` + style.transform;
    }

    return style;
})
</script>

<template>
    <img :src="onTop ? 'src/assets/latch.png' : 'src/assets/latch_bottom.png'" :width="width" :style='style'>
</template>
