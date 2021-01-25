<template>
    <div class="header-comp">
        <h1>{{ restaurantName }}</h1>
    </div>
</template>

<script>
export default {
    name: "header-comp",
    data() {
        return {};
    },
    props: {
        restaurantName: {
            type: String,
            default: "Nha hang Bien Dong",
        },
    },
};
</script>

<style>
</style>