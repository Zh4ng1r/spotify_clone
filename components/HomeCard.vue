<template>
    <div>
        <div class="card__items">
            <NuxtLink v-for="item in playlistItems" :key="item.id" :to="`/playlist/${item.id}`">
                <div class="card__item">
                    <img :src="item.images[0].url" class="card__item--img" />
                    <div class="card__item--text">
                        <div class="card__item--text--title">{{ item.name }}</div>
                        <div class="card__item--text--subTitle">{{ item.label }}</div>
                    </div>
                </div>
            </NuxtLink>
        </div>
    </div>
</template>
  
<script setup>
import { ref, defineProps } from 'vue';

const props = defineProps(['playlistItems']);
</script>
  
<style lang="scss" scoped>
.card {
    &__items {
        display: flex;
        align-items: center;
        flex-wrap: wrap;
        gap: 30px;
    }

    &__item {
        background-color: #181818;
        padding: 20px;
        border-radius: 15px;
        width: 183px;
        height: 273px;
        overflow: hidden;

        &:hover {
            background-color: #282828;
        }

        &--img {
            width: 100%;
            height: 150px;
            margin-bottom: 10px;
            object-fit: cover;
            border-radius: 8px;
        }

        &--text {
            font-weight: 600;
            color: #ffffff;

            &--title {
                margin-bottom: 10px;
                font-size: 16px;
            }

            &--subTitle {
                font-size: 14px;
                color: #b3b3b3;
            }
        }
    }
}
</style>
  