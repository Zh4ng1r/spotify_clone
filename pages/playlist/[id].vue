<template>
    <div class="playlist-page">
        <h1>Плейлист ID: {{ id }}</h1>
        <div v-if="playlist">
            <h2>{{ playlist.name }}</h2>
            <div v-for="track in playlist.tracks.items" :key="track.id">
                <p>{{ track.track.name }}</p>
            </div>
        </div>
        <div v-else>
            <p>Загрузка...</p>
        </div>
    </div>
</template>
  
<script setup>
import { ref, onMounted } from 'vue';
import { getToken } from '../../api'
import axios from 'axios';

const { id } = useRoute().params
const playlist = ref(null);

onMounted(async () => {
    playlist.value = await fetchPlaylist(id); // Use id directly
});

const fetchPlaylist = async (id) => {
    try {
        const token = await getToken();
        const response = await axios.get(`https://api.spotify.com/v1/albums/${id}/tracks `, {
            headers: { 'Authorization': 'Bearer ' + token }
        });
        return response.data;
    } catch (error) {
        console.error(error);
        return null;
    }
};
</script>
  
<style lang="scss"></style>
  