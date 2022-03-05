<script setup>
import { computed } from 'vue';
import { getRandomNumberBetween } from '../../utils';

const props = defineProps({
    progress: Number,
    width: Number
})

const random = getRandomNumberBetween(-5, 5);

const progress = computed(() => props.progress / 100)

const style = computed(() => ({
    transform: `translate(0px, ${progress.value * 15 * -1}px)` + ` rotate(${progress.value * random}deg)`,
    height: '100%'
}))
</script>

<template>
    <img src="src/assets/spring.svg" :width="width" :style='style'>
</template>