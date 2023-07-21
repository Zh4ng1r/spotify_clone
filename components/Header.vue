<template>
    <div class="Header__layout">
        <div class="Header__layout--icons">
            <button type="button" class="Header__layout--buttonLeft">
                <ChevronLeft class="Header__layout--left" />
            </button>
            <button type="button" class="Header__layout--buttonRight">
                <ChevronRight class="Header__layout--right" />
            </button>
        </div>
        <button type="button" class="DropDown" @click="openMenu = !openMenu">
            <div v-if="accessToken" class="DropDown__inner">
                <img src="https://yt3.ggpht.com/yti/AOXPAcUY9uKYPEYyAMA39LfWxGi_4x-51ypzAZFRtsmQiw=s88-c-k-c0x00ffffff-no-rj"
                    class="DropDown--image" />
                <div class="DropDown--text">Zhangir</div>
                <ChevronDown v-if="!openMenu" :size="24" class="DropDown--icon" />
                <ChevronUp v-if="openMenu" :size="24" class="DropDown--icon" />
            </div>
        </button>
        <span v-if="openMenu" class="DropDown__items">
            <ul class="DropDown__list">
                <li class="DropDown_item">Profile</li>
                <li class="DropDown_item">LogOut</li>
            </ul>
        </span>
    </div>
</template>
  
<script setup>
import { ref } from 'vue';
import ChevronUp from 'vue-material-design-icons/ChevronUp.vue';
import ChevronDown from 'vue-material-design-icons/ChevronDown.vue';
import ChevronLeft from 'vue-material-design-icons/ChevronLeft.vue';
import ChevronRight from 'vue-material-design-icons/ChevronRight.vue';

const openMenu = ref(false);
const accessToken = ref('');

if (process.client) {
    accessToken = localStorage.getItem('spotify_access_token');
    console.log(accessToken)
}
</script>
  
<style lang="scss" scoped>
@import './assets/helpers/default';

.Header {
    &__layout {
        width: calc(100% - 240px);
        height: 60px;
        position: fixed;
        right: 0;
        z-index: 20;
        background-color: #040404;
        display: flex;
        align-items: center;
        justify-content: space-between;

        &--icons {
            display: flex;
            align-items: center;
            margin-left: 6px;
        }

        &--buttonLeft,
        &--buttonRight {
            background: #1db954;
            padding: 1px;
            cursor: pointer;
            width: 32px;
            height: 32px;
            border: none;
            border-radius: 50%;

            &:focus {
                outline: none;
            }
        }

        &--left,
        &--right {
            color: #ffffff;
        }
    }
}

.DropDown {
    margin-right: 8px;
    margin-top: 5px;
    cursor: pointer;
    border: none;
    padding-left: 0px;
    border-radius: 9999px;
    background-color: #040404;
    color: #ffffff;
    font-size: 14px;
    font-weight: 600;

    &__inner {
        display: flex;
        align-items: center;
    }

    &--image {
        height: 32px;
        width: 32px;
        border-radius: 50%;
        margin-right: 8px;
    }

    &--text {
        margin-right: 8px;
    }

    &--icon {
        width: 24px;
        height: 24px;
    }
}

.DropDown__items {
    position: absolute;
    width: 176px;
    background: #282828;
    box-shadow: 0 2px 5px rgba(0, 0, 0, 0.2);
    z-index: 50;
    border-radius: 0.125rem;
    top: 60px;
    right: 35px;
    padding: 1px;
    cursor: pointer;
    color: #ffffff;
    font-size: 14px;
    font-weight: 600;

    &__list {
        padding: 0;
        margin: 0;
        list-style: none;
    }

    &__item {
        padding: 10px;
        border-bottom: 1px solid #585858;

        &:hover {
            background-color: #3e3d3d;
        }
    }
}
</style>
  