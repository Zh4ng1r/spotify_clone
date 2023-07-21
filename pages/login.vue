<template>
    <div id="app">
        <div v-if="!access_token" id="login">
            <h1>This is an example of the Authorization Codlow</h1>
            <a href="/login" class="btn btn-primary">Log in with Spotify</a>
        </div>
        <div v-else id="loggedin">
            <div id="user-profile">
                <h1>Logged in as {{ userProfile.display_name }}</h1>
                <div class="media">
                    <div class="pull-left">
                        <img class="media-object" width="150" :src="userProfile.images[0].url" />
                    </div>
                    <div class="media-body">
                        <dl class="dl-horizontal">
                            <dt>Display name</dt>
                            <dd class="clearfix">{{ userProfile.display_name }}</dd>
                            <dt>Id</dt>
                            <dd>{{ userProfile.id }}</dd>
                            <dt>Email</dt>
                            <dd>{{ userProfile.email }}</dd>
                            <dt>Spotify URI</dt>
                            <dd><a :href="userProfile.external_urls.spotify">{{ userProfile.external_urls.spotify }}</a>
                            </dd>
                            <dt>Link</dt>
                            <dd><a :href="userProfile.href">{{ userProfile.href }}</a></dd>
                            <dt>Profile Image</dt>
                            <dd class="clearfix"><a :href="userProfile.images[0].url">{{ userProfile.images[0].url }}</a>
                            </dd>
                            <dt>Country</dt>
                            <dd>{{ userProfile.country }}</dd>
                        </dl>
                    </div>
                </div>
            </div>
            <div id="oauth">
                <h2>oAuth info</h2>
                <dl class="dl-horizontal">
                    <dt>Access token</dt>
                    <dd class="text-overflow">{{ access_token }}</dd>
                    <dt>Refresh token</dt>
                    <dd class="text-overflow">{{ refresh_token }}</dd>
                </dl>
            </div>
            <button class="btn btn-default" id="obtain-new-token" @click="obtainNewToken">Obtain new token using the refresh
                token</button>
        </div>
    </div>
</template>
  
<script>
import axios from 'axios';

export default {
    data() {
        return {
            access_token: true,
            refresh_token: '',
            userProfile: {},
        };
    },
    mounted() {
        this.handleAuthentication();
    },
    methods: {
        handleAuthentication() {
            const params = this.getHashParams();
            this.access_token = params.access_token;
            this.refresh_token = params.refresh_token;

            if (this.access_token) {
                this.getUserProfile();
            }
        },
        getHashParams() {
            const hashParams = {};
            const r = /([^&;=]+)=?([^&;]*)/g;
            const q = window.location.hash.substring(1);
            let e;
            while ((e = r.exec(q))) {
                hashParams[e[1]] = decodeURIComponent(e[2]);
            }
            return hashParams;
        },
        getUserProfile() {
            const headers = {
                'Authorization': 'Bearer ' + this.access_token
            };

            axios.get('https://api.spotify.com/v1/me', { headers })
                .then(response => {
                    this.userProfile = response.data;
                })
                .catch(error => {
                    console.error(error);
                });
        },
        obtainNewToken() {
            const refresh_token = this.refresh_token;

            axios.get('/refresh_token?refresh_token=' + refresh_token)
                .then(response => {
                    this.access_token = response.data.access_token;
                })
                .catch(error => {
                    console.error(error);
                });
        },
    },
};
</script>
  
<style>
.text-overflow {
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
    width: 500px;
}
</style>
  