<script setup>import { computed } from 'vue';

const props = defineProps({
    onTop: Boolean,
    progress: Number
})

function getRandomNumberBetween(min,max){
    return Math.floor(Math.random()*(max-min+1)+min);
}

const random = getRandomNumberBetween(-2, 2);

const progress = computed(() => props.progress / 100)
const sign = computed(() => props.onTop ? -1 : 1);

const style = computed(() => ({
    transform: (props.onTop ? `translate(0px, ${progress.value * 15 * -1}px)` : '') + ` rotate(${(props.onTop ? 0 : 180) + (progress.value * (3 + random) * sign.value)}deg)`
}))
</script>

<template>
    <img :src="onTop ? 'src/assets/latch.png' : 'src/assets/latch_bottom.png'" width="35" :style='style'>
</template>
