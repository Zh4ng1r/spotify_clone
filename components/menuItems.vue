<script setup>
import { defineProps, ref, watchEffect } from 'vue';
import { useRoute } from 'vue-router';

const props = defineProps({
    iconString: String,
    iconSize: Number,
    pageUrl: String,
    name: String
});

const route = useRoute();
const icon = ref(null);
const textIsHover = ref(false);

watchEffect(() => {
    if (route.path === props.pageUrl) {
        icon.value = `${props.iconString}-active`;
        textIsHover.value = true;
    } else {
        icon.value = `${props.iconString}-inactive`;
        textIsHover.value = false;
    }
});

const isHover = () => {
    if (icon.value === `${props.iconString}-active`) return;

    if (icon.value === `${props.iconString}-inactive`) {
        icon.value = `${props.iconString}-inactive-hover`;
        textIsHover.value = true;
    } else if (icon.value === `${props.iconString}-inactive-hover`) {
        icon.value = `${props.iconString}-inactive`;
        textIsHover.value = false;
    }
};
</script>

<template>
    <li class="items" @mouseenter="isHover" @mouseleave="isHover">
        <img :width="iconSize" :src="`../assets/images/${icon}.png`" />
        <div class="items__text">
            <span :class="{ active: $route.path === pageUrl }">{{ props.name }}</span>
        </div>
    </li>
</template>

<style lang="scss" scoped>
.items {
    display: flex;
    align-items: center;
    justify-content: flex-start;
    padding-bottom: 4px;
    cursor: pointer;
    margin-left: 8px;
    margin-bottom: 10px;

    &__text {
        color: #b3b3b3;
        font-size: 16px;
        font-weight: 500;
        margin-left: 12px;
        transition: color 0.3s;

        &:hover {
            color: white;
        }
    }
}

.active {
    color: white;
    font-weight: bold;
}
</style>
