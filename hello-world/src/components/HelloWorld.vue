<template>
    <div class="hello">
        <h1>{{ msg }}</h1>
        <h1>{{ count }}</h1>
        <button @click="addOne()">Click me!</button>
    </div>
</template>

<script>
export default {
    data() {
        return {
            count: 0,
        };
    },
    name: "HelloWorld",
    props: {
        msg: {
            type: String,
            default: "Welcome to my Vue app",
        },
    },
    methods: {
        addOne() {
            this.count++;
        },
    },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
    margin: 40px 0 0;
}
ul {
    list-style-type: none;
    padding: 0;
}
li {
    display: inline-block;
    margin: 0 10px;
}
a {
    color: #42b983;
}
</style>
