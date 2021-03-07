<template>
    <div class="catalogItem">
        <p class="catalogItem__name">{{product_data.name}}</p>
        <p class="catalogItem__price">Price: {{product_data.price}}</p>
        <button class="catalogItem__buy_btn btn" @click="addToCart">Buy</button>
    </div>
</template>

<script>
    export default {
        name: "catalog-item",
        props: {
            product_data: {
                type: Object,
                default() {
                    return {}
                }
            }
        },
        methods: {
            addToCart() {
                this.$emit('addToCart', this.product_data)
            }
        },
        mounted() {
            this.$set(this.product_data, 'quantity', 1)
        }
    }
</script>

<style lang="scss">
.catalogItem {
    flex-basis: 25%;
    box-shadow: 0 0 8px 0 #e0e0e0;
    padding: 16px;
    margin-bottom: 16px;
    &__image {
        width: 100px;
    }
}
</style>