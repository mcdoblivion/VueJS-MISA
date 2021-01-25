<template>
    <div id="app">
        <header-comp restaurantName="Nha hang Bien Dong" />
        <left-bar />
        <content />
    </div>
</template>

<script>
import Content from "./components/Content.vue";
import Header from "./components/Header.vue";
import HelloWorld from "./components/HelloWorld.vue";
import LeftBar from "./components/LeftBar.vue";

export default {
    name: "App",
    components: {
        HelloWorld,
        Header,
        Content,
        LeftBar,
    },
};
</script>

<style>
#app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
}
</style>
