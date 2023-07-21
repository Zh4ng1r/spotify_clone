<template>
    <Header />
    <sideNav />
    <main class="mainBlock">
        <NuxtPage />
    </main>
</template>

<style lang="scss" scoped>
.mainBlock {
    position: fixed;
    right: 0;
    top: 60px;
    width: calc(100% - 240px);
    overflow: auto;
    height: 100%;
    background: linear-gradient(to bottom, #1C1C1C, black);

    &__forHeader {
        margin-top: 70px;
    }

    &__forFooter {
        margin-bottom: 100px;
    }
}
</style>