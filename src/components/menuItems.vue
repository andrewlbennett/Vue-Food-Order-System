<template>
    <div id="menu-items">
        <button class="btn">Add Cheeseburger - 6.99</button>
        <button class="btn">Add Fries - 2.39</button>
        <button class="btn">Add Drink - 1.29</button>
        <button class="btn">Add Cheesecake - 3.99</button>
    </div>
</template>

<script>
export default {
    name: 'menuItems'
}
</script>

<style lang="scss">
    #menu-items {
        flex: 1 0 75%;
        padding: 2rem;
    }
</style>