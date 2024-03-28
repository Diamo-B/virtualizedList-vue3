<script lang="ts">
import { defineComponent, PropType } from "vue";

export default defineComponent({
    props: {
        filteredItems: {
            type: Array as PropType<string[]>,
            required: true,
        },
        scrollTop: {
            type: Number as PropType<number>,
            required: true,
        }
    },
});
</script>

<template>
    <p
        v-for="(item, index) in filteredItems" :key="index"
        :class="`my-5 border-2 rounded-lg py-3 text-center h-16 w-full absolute top-${Math.floor(scrollTop/64)+index}`"
    >
        {{ item }}
    </p>
</template>
