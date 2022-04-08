<template>
    <section class="container-products">
        <div v-if="products && products.length" class="products">
            <div class="product" v-for="product in products" :key="product.id">
                <router-link to="/">
                        <img v-if="product.fotos" :src="product.fotos[0].src" :alt="product.fotos[0].titulo">
                        <p class="price">{{product.preco}}</p>
                        <h2 class="title">{{product.nome}}</h2>
                        <p>{{product.descricao}}</p>
                </router-link>
            </div>
        </div>
        <div v-else-if="products && products.length === 0">
            <p class="sem-resultados">Busca sem resultados</p>
        </div>
    </section>
</template>

<script>
import { api } from '@/services'
import { serialize } from '@/helpers'

export default {
    name: "ProductsList",
    data(){
        return {
            products: null,
            productsForPage: 9
        }
    },
    computed: {
        url() {
            const query = serialize(this.$route.query)
            return `/produto?_limite=${this.productsForPage}${query}`
        }
    },
    methods: {
        getProducts() {
            api.get(this.url).then(response => {
                this.products = response.data;
            });
            
        }
    },
    watch: {
        url(){
            this.getProducts();
        }
    },
    created() {
        this.getProducts();
    }
}
</script>

<style scoped>
    .container-products {
        max-width: 1000px;
        margin: 0 auto;
    }
    .products{
        display: grid;
        grid-template-columns: repeat(3, 1fr);
        grid-gap: 30px;
    }

    .product{
        box-shadow: 0 4px 8px rgba(30, 60, 90, 0.1);
        padding: 20px;
        background: #fff;
        border-radius: 4px;
        transition: all 0.2s;
    }

    .product:hover {
        box-shadow: 0 6px 12px rgba(30, 60, 90, 0.2);
        transform: scale(1.1);
        position: relative;
        z-index: 1;
    }

    .product img {
        border-radius: 4px;
        margin-bottom: 20px;
    }

    .title {
        margin-bottom: 10px;

    }

    .price {
        font-weight: bold;
        color: #e80;

    }

    .sem-resultados {
        text-align: center;
    }
</style>