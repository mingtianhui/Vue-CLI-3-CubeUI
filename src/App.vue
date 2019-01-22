<template>
    <div id="app">
        <keep-alive>
            <router-view v-if="$route.meta.keepAlive" :key="$route.fullPath"></router-view>
        </keep-alive>
        <router-view v-if="!$route.meta.keepAlive" :key="$route.fullPath"></router-view>
    </div>
</template>

<style lang="stylus">
    @import "stylus/base/common.styl";
</style>
<style>
    @import "stylus/base/sprites.css";
</style>
