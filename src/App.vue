<template>
    <div id="app">
        <order></order>
    </div>
</template>

<script>
import order from './components/order.vue'
export default {
    name: 'app',
    components: {
        order
    },
    data () {
        return {

        }
    }
}
</script>

<style lang="scss">
    :root {
        box-sizing: border-box;
        font-size: 16px;
        font-family: 'Open Sans', Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        color: #111;
        background-color: #F4F6F8;
    }

    *,
    *::before,
    *::after {
        box-sizing: inherit;
    }

    body,
    html {
        width: 100vw;
        height: 100vh;
        overflow: hidden;
        margin: 0;
        padding: 0;
    }

    body {
        line-height: 1.5;
    }

    #app {
        display: flex;
        width: 100vw;
        height: 100vh;
        overflow: hidden;
    }

    ul {
        list-style: none;
        margin: 0;
        padding: 0;
    }

    p {
        margin-top: 0;
    }
</style>
