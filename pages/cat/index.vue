<template>
    <article>
        <img v-bind="{ ...image_info }" />
    </article>
</template>

<script setup>
import { ref, computed } from "vue";

const cat = ref([{
    "id": "",
    "url": "",
    "width": 0,
    "height": 0
}]);

const image_info = computed( () => {
    const item = cat.value[0];
    return {
        src: item.url,
        alt: item.id,
        width: item.width,
        height: item.height,
    };
});

const set_cat = (data = []) => {
    cat.value = data;
};
const ajax_cat = () => {
    fetch("https://api.thecatapi.com/v1/images/search").then( r => r.json() ).then( set_cat );
};

ajax_cat();
</script>
