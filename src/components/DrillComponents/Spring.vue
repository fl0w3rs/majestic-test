<script setup>
import { computed } from 'vue';

const props = defineProps({
    progress: Number,
    width: Number
})

function getRandomNumberBetween(min,max){
    return Math.floor(Math.random()*(max-min+1)+min);
}

const random = getRandomNumberBetween(-5, 5);

const progress = computed(() => props.progress / 100)

const style = computed(() => ({
    transform: `translate(0px, ${progress.value * 15 * -1}px)` + ` rotate(${progress.value * random}deg)`
}))
</script>

<template>
    <img src="src/assets/spring.png" :width="width" :style='style'>
</template>