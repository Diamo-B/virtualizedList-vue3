<script setup lang="ts">
import Item from "./components/Item.vue";
import { Ref, onBeforeMount, onMounted, ref, watch } from "vue";


const containerRef = ref<HTMLDivElement>();
const showcaseContainerHeight = ref(0);
const scrollPosition = ref(0);
const items: Ref<string[]> = ref([]);
const startIndex = ref(0);
const endIndex = ref(0);
const filteredItems: Ref<string[]> = ref([]);

onBeforeMount(()=>{
    for (let i = 0; i <= 100; i++) {
        items.value.push(i.toString());
    }
})

onMounted(() => {
    showcaseContainerHeight.value = containerRef?.value?.clientHeight || 0;
    updateIndexes();
});

const updateIndexes = () => {
    scrollPosition.value = containerRef?.value?.scrollTop || 0;
    startIndex.value = Math.floor(scrollPosition.value / 64); 
    endIndex.value = Math.min(items.value.length-1, Math.floor((scrollPosition.value + showcaseContainerHeight.value) / 64));
    filteredItems.value = items.value.slice(startIndex.value, endIndex.value+1);
}; 

watch([startIndex, endIndex],()=>{
    console.log("start: ",startIndex.value," / End: ",endIndex.value);
    
})

</script>

<template>
    <div class="h-full flex flex-col justify-center items-center py-10 ">
        <div
            ref="containerRef"
            class="overflow-y-auto h-64 border-2 w-1/3 rounded-lg relative"
            @scroll="updateIndexes"
        >
            <div class="w-full font-bold text-2xl relative" :style="{height: `${items.length*64}px`}">
              <Item :filtered-items="filteredItems" :scroll-top="scrollPosition"/>
            </div>
        </div>
    </div>
</template>
