<template>
    <form>
        <input name="search" id="search" type="text" v-model="search">
        <input type="submit" id="lupa" value="search" @click.prevent="productSearch">
    </form>
</template>

<script>
export default {
    name: "ProductsSearch",
    data() {
        return {
            search: ""
        }
    },
    methods: {
        productSearch() {
            this.$router.push({ query: { q: this.search }})
        }
    }
}
</script>

<style>
    form{
        margin: 2rem auto;
        text-align: center;
    }
</style>