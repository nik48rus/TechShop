<template>
    <div class="cartItem">
        <p>{{cart_item_data.name}}</p>
        <p>{{cart_item_data.price}}</p>
        <p>{{cart_item_data.article}}</p>
        <div>
            <p>Quantity: </p>
            <span>
                <span @click="decrementItem">-</span>
                {{cart_item_data.quantity}}
                <span @click="incrementItem">+</span>
            </span>
        </div>

        <button @click="deleteFromCart">X</button>
    </div>
</template>

<script>
    export default {
        name: "cartItem",
        props: {
            cart_item_data: {
                type: Object,
                default() {
                    return {};
                }
            }
        },
        data() {
            return {};
        },
        mounted() {},
        methods: {
            deleteFromCart() {
                this.$emit('deleteFromCart');
            },
            incrementItem() {
                this.$emit('increment');
            },
            decrementItem() {
                this.$emit('decrement');
            }
        }
    }
</script>

<style lang="scss">
.cartItem {
    display: flex;
    flex-wrap: nowrap;
    justify-content: space-between;
    align-items: center;
    box-shadow: 0 0 8px 0 #e0e0e0;
    padding: 16px;
    margin-bottom: 16px;
}
</style>