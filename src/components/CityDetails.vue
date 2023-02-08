<template>
    <p class="text-gray-500 mt-4 mb-2 flex">
        <RectangleGroupIcon class="h-5 w-5 text-gray-500 mr-2" aria-hidden="true" />
        {{ city.name }}
    </p>
    <img :src="city.image" alt="" />
</template>
<script setup>
import { RectangleGroupIcon } from '@heroicons/vue/24/outline';
import { defineProps, computed } from 'vue';
const props = defineProps({
    city: {
        type: Object,
        default: () => { }
    }
})

const city = computed(() => props.city)
</script>