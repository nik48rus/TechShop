<template>
    <div class="catalog">
        <router-link :to="{name: 'cart', params: {cart_data: CART}}">
            <div class="catalog__link_to_cart">Cart: {{CART.length}}</div>
        </router-link>

        <h1>Catalog</h1>
        <div class="catalog__list">
            <catalogItem
                    v-for="product in PRODUCTS"
                    :key="product.article"
                    v-bind:product_data="product"
                    @addToCart="addToCart"
            />
        </div>
    </div>
</template>

<script>
    import catalogItem from "./catalogItem";
    import {mapActions, mapGetters} from 'vuex';

    export default {
        name: "catalog",
        components: {
            catalogItem
        },
        data() {
            return {}
        },
        computed: {
            ...mapGetters(['PRODUCTS', 'CART'])
        },
        methods: {
            ...mapActions(['GET_PRODUCTS_FROM_API', 'ADD_TO_CART']),
            addToCart(data) {
                this.ADD_TO_CART(data);
            }
        },
        mounted() {
            this.GET_PRODUCTS_FROM_API()
        },
    }
</script>

<style lang="scss">
.catalog{
    &__list{
        display: flex;
        flex-wrap: wrap;
        justify-content: space-between;
        align-items: center;
    }
    &__link_to_cart {
        position: absolute;
        top: 10px;
        right: 10px;
        padding: 16px;
        border: solid 1px gray;
    }
}
</style>