<template>
    <section class="container-products">
        <div v-for="product in products" :key="product.id">
           <img v-if="product.fotos" :src="product.fotos[0].src" :alt="product.fotos[0].titulo">
            <p class="price">{{product.preco}}</p>
            <h2 class="title">{{product.nome}}</h2>
            <p>{{product.descricao}}</p>
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

<style>
    
</style>