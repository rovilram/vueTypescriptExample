<template lang="pug">
.container
    .nav-bar
    #app
        .cart
            p Cart({{ cart.length }})
        product(:premium='true', @add-to-card='increaseCart', @remove-from-card='decreaseCart')
        ProductReview(@add-review='addReview')
        ReviewList(:reviews='reviews')
</template>

<style lang="scss">
#app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
}

#nav {
    padding: 30px;

    a {
        font-weight: bold;
        color: #2c3e50;

        &.router-link-exact-active {
            color: #42b983;
        }
    }
}
</style>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import product from './components/product.vue';
import ProductReview from './components/ProductReview.vue';
import ReviewList from './components/ReviewList.vue';

@Component({
    components: { product, ProductReview, ReviewList }
})
export default class App extends Vue {
    cart: number[] = [];
    reviews: string[] = [];

    increaseCart(id: number) {
        this.cart.push(id);
    }
    decreaseCart(id: number) {
        this.cart = this.cart.filter((_, i) => this.cart.findIndex((el) => el === id) != i);
    }
    addReview(review: string) {
        this.reviews.push(review);
    }
}
</script>
