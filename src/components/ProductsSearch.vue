<template>
    <form>
        <input name="search" id="search" placeholder="Buscar..." type="text" v-model="search">
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

<style scoped>
    form{
        margin: 2rem auto;
        text-align: center;
        max-width: 600px;
        margin: 30px auto 60px auto;
        position: relative;
    }

    #search {
        width: 100%;
        box-shadow: 0 4px 8px rgba(30, 60, 90, 0.1);
        padding: 20px;
        border: none;
    }

    #search:focus,
    #search:hover {
        transform: scale(1.1);
    }

    #lupa {
        width: 62px;
        height: 62px;
        background: url("../assets/search.svg") no-repeat center center;
        text-indent: -150px;
        border: none;
        cursor: pointer;
        position: absolute;
        top: 0;
        right: 0;
        box-shadow: none;
    }
</style>