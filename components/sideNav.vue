<template>
    <div class="sideNav">
        <NuxtLink to="/">
            <img src="../assets/images/spotify-logo.png" alt="" class="sideNav__logo">
        </NuxtLink>
        <div class="sideNav__items">
            <NuxtLink to="/">
                <MenuItems :iconSize="23" name="Home" iconString="home" pageUrl="/" />
            </NuxtLink>
            <NuxtLink to="/search">
                <MenuItems :iconSize="23" name="Search" iconString="search" pageUrl="/search" />
            </NuxtLink>
            <NuxtLink to="/library">
                <MenuItems :iconSize="23" name="Library" iconString="library" pageUrl="/library" />
            </NuxtLink>
            <div class="sideNav__text">
                <NuxtLink to="/playlist">
                    <MenuItems :iconSize="24" name="Create Playlist" iconString="playlist" pageUrl="/playlist" />
                </NuxtLink>
                <NuxtLink to="/liked">
                    <MenuItems :iconSize="27" name="Liked Songs" iconString="liked" pageUrl="/liked"
                        class="sideNav__liked" />
                </NuxtLink>
            </div>
        </div>
        <div class="sideNav__border"></div>
        <ul class="sideNav__playlists">
            <li class="sideNav__li">My playlist#1</li>
            <li class="sideNav__li">My playlist#2</li>
            <li class="sideNav__li">My playlist#3</li>
            <li class="sideNav__li">My playlist#4</li>
        </ul>
    </div>
</template>
    
<style lang="scss" scoped>
.sideNav {
    height: 100%;
    padding: 20px;
    width: 240px;
    position: fixed;
    z-index: 50;
    background-color: #040404;
    color: #fff;
    font-family: 'Arial', sans-serif;

    &__logo {
        width: 125px;
        height: 40px;
        margin-bottom: 20px;
        object-fit: contain;
    }

    &__items {
        display: flex;
        flex-direction: column;
        align-items: flex-start;
        margin-bottom: 25px;
    }

    &__text {
        padding-top: 15px;
        padding-bottom: 3px;
        margin-bottom: 15px;
    }

    &__border {
        border: 1px solid #282828;
        margin-bottom: 20px;
    }

    &__li {
        font-weight: 600;
        font-size: 13px;
        margin-top: 10px;
        color: #b3b3b3;
        cursor: pointer;

        &:hover {
            color: #fff;
        }
    }

    &__playlists {
        list-style: none;
        padding: 0;
        margin: 0;
    }
}
</style>
  