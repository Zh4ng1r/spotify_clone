<script setup>

</script>

<template>
    <div class="home">
        <button class="home__button">
            Podcast
        </button>
    </div>
</template>

<style lang="scss" scoped>
.home {
    padding: 8px;

    &__button {
        color: white;
        font-size: 1.5rem;
        line-height: 2rem;
        font-weight: 600;
        cursor: pointer;

        &:hover {
            text-decoration: underline;
        }
    }
}
</style>