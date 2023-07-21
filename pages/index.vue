<template>
    <div class="home">
        <button class="home__button" @click="console.log(playlistItems)">
            Для Вас
        </button>
        <div class="home__list">
            <HomeCard :playlistItems="playlistItems" />
        </div>
    </div>
</template>

<script setup>
// import { getToken } from '../api';
import axios from 'axios';
import { ref, onMounted } from 'vue';

const token = ref('');
const playlistItems = ref([]);
// console.log(playlistItems.value)
// 
// onMounted(async () => {
    // token.value = await getToken();
    // getData();
// });
// 
// const getData = async () => {
    // try {
        // const response = await axios.get('https://api.spotify.com/v1/me', {
            // headers: { 'Authorization': 'Bearer ' + token.value }
        // });
        // playlistItems.value = response.data.albums;
    // } catch (error) {
        // console.error(error);
    // }
// 
// };
</script>

<style lang="scss" scoped>
.home {

    padding: 16px;

    &__button {
        padding-top: 10px;
        color: white;
        font-size: 1.5rem;
        line-height: 2rem;
        font-weight: 600;
        cursor: pointer;
        margin-bottom: 16px;

        &:hover {
            text-decoration: underline;
        }
    }
}
</style>