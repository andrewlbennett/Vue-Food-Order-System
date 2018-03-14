<template>
    <div id="order-screen">
        <menuItems></menuItems>
        <receipt></receipt>
    </div>
</template>

<script>
import receipt from './receipt.vue';
import menuItems from './menuItems.vue';
export default {
    name: 'order',
    components: {
        receipt,
        menuItems
    }
}
</script>

<style lang="scss">
    #order-screen {
        display: flex;
        width: 100vw;
        height: 100vh;
        overflow: hidden;
    }
</style>
