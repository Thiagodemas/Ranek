<template>
    <ul v-if="totalPage > 1">
        <li v-for="page in totalPage" :key="page">
            <router-link :to="{query: query(page)}">{{page}}</router-link>
        </li>
    </ul>
</template>

<script>
export default {
    props: {
        productsForPage: {
            type: Number,
            default: 1
        },
        productsTotal: {
            type: Number,
            default: 1
        }
    },
    methods: {
        query(page) {
            return {
                ...this.$route.query,
                _page: page,
            }
        }
    },
    computed: {
        totalPage() {
           const total = this.productsTotal / this.productsForPage
           return total !== Infinity ? Math.ceil(total) : 0;
        }
    }
}
</script>

<style>
    ul {
        grid-column: 1 / -1;
    }

    li {
        display: inline-block;
    }

    li a {
        padding: 2px 8px;
        border-radius: 2px;
        margin: 4px;
    }

    li a.router-link-exact-active,
    li a:hover {
        background: #87f;
        color: #fff;
    }
</style>