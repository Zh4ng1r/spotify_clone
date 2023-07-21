<template>
    <div class="auth-page">
        <h1>Авторизация через Spotify</h1>
        <a v-if="!accessToken" class="login-button" :href="authorizeUrl">Войти через Spotify</a>
        <p v-else>Вы успешно авторизовались.</p>
    </div>
</template>
<script setup>
import { ref, onMounted } from 'vue';
import axios from 'axios';

const clientId = 'c3c25e9db5054c85bc138ed3d1208148';
const client_secret = '47fb691623644676bc634127a9681de2';
const redirectUri = 'http://localhost:3000/auth';
const scopes = 'user-read-private user-read-email';

const authorizeUrl = `https://accounts.spotify.com/authorize?client_id=${clientId}&response_type=code&redirect_uri=${encodeURIComponent(
    redirectUri
)}&scope=${encodeURIComponent(scopes)}`;

const route = useRoute();
const router = useRouter();
const accessToken = ref('');

const getAccessToken = async (code) => {
    let body = "grant_type=authorization_code";
    body += "&code=" + code;
    body += "&redirect_uri=" + encodeURIComponent(redirectUri);
    body += '&client_id=' + clientId;
    body += "&client_secret=" + client_secret;

    try {
        const response = await axios.post(
            'https://accounts.spotify.com/api/token',
            body,
            {
                headers: {
                    'Content-Type': 'application/x-www-form-urlencoded',
                    'Authorization': 'Basic ' + btoa(clientId + ':' + client_secret).toString()
                }
            }
        );

        const responseData = response.data;
        accessToken.value = responseData.access_token;

        if (process.client) {
            localStorage.setItem('spotify_access_token', accessToken.value);
        }

    } catch (error) {
        console.error(error);
    }
};

onMounted(async () => {
    console.log('hey', window.location);
    if (route.query.code) {
        const code = route.query.code;
        console.log('code', code);
        await getAccessToken(code);
        router.push({ query: null })
    }

});
</script>

<style lang="scss">
.auth-page {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    height: 100vh;
    background-color: #000000;
    color: #fff;
    font-family: 'Montserrat', sans-serif;

    .logo {
        width: 120px;
        height: 120px;
        margin-bottom: 20px;
        object-fit: contain;
    }

    h1 {
        font-size: 24px;
        margin-bottom: 20px;
    }

    .login-button {
        padding: 12px 24px;
        font-size: 16px;
        font-weight: 600;
        background-color: #1db954;
        color: #fff;
        text-decoration: none;
        border: none;
        border-radius: 4px;
        cursor: pointer;
        transition: background-color 0.3s ease;

        &:hover {
            background-color: #199e4d;
        }
    }
}
</style>
