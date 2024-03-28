<script setup lang="ts">
    interface Props  {
        filteredItems: string[],
        scrollTop: number
    }
 defineProps<Props>();
</script>

<template>
    <p
        v-for="(item, index) in filteredItems" :key="index"
        class="w-full h-16 px-10 absolute" :style="{top: `${(Math.floor(scrollTop/64)+index)*64}px`}"
    >
        {{ item }}
    </p>
</template>
