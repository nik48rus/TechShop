<template>
    <div class="cart">
        <router-link :to="{name: 'catalog'}">
            <div class="cart__link_to_catalog">Back to Catalog</div>
        </router-link>
        <h1>Cart:</h1>
        <p v-if="!cart_data.length">No products</p>
        <cartItem
                v-for="(item, index) in cart_data"
                :key="item.name"
                :cart_item_data="item"
                @deleteFromCart="deleteFromCart(index)"
                @increment="increment(index)"
                @decrement="decrement(index)"
        />
        <div class="cart__total">
            <p class="total__name">Total:</p>
            <p>{{cartTotalCost}} р</p>
        </div>
    </div>
</template>

<script>
    import cartItem from "./cartItem";
    import {mapActions} from 'vuex';
    export default {
        name: "cart",
        components: {
            cartItem
        },
        props: {
            cart_data: {
                type: Array,
                default() {
                    return [];
                }
            }
        },
        data() {
            return {};
        },
        computed: {
            cartTotalCost() {
                let result = [];

                if(this.cart_data.length) {
                    for (let item of this.cart_data) {
                        result.push(item.price * item.quantity);
                    }

                    result = result.reduce(function (sum, el) {
                        return sum + el;
                    });
                    return result;
                } else {
                    return 0;
                }
            }
        },
        methods: {
            ...mapActions(['DELETE_FROM_CART', 'INCREMENT_CART_ITEM', 'DECREMENT_CART_ITEM']),
            deleteFromCart(index) {
                this.DELETE_FROM_CART(index);
            },
            increment(index) {
                this.INCREMENT_CART_ITEM(index);
            },
            decrement(index) {
                this.DECREMENT_CART_ITEM(index);
            }
        }
    }
</script>

<style lang="scss">
.cart{
    &__total {
        position: fixed;
        bottom: 0;
        right: 0;
        left: 0;
        padding: 16px 24px;
        display: flex;
        justify-content: center;
        background: #017a12;
        color: #fff;
        font-size: 20px;
    }
    &__link_to_catalog {
        position: absolute;
        top: 10px;
        right: 10px;
        padding: 16px;
        border: solid 1px gray;
    }
    .total__name {
        margin-right: 16px;
    }
}
</style>