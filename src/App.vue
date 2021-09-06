<template lang="pug">
.container
    .nav-bar
    #app
        .cart
            p Cart({{ cart.length }})
        product(@add-to-card='increaseCart', @remove-from-card='decreaseCart')
        ProductTabs(:reviews='reviews', :premium='true', :details='details')
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
import eventBus from './components/eventBus';
import product from './components/product.vue';
import ProductTabs from './components/ProductTabs.vue';

export interface reviewInterface {
    name: string;
    review: string;
    rating: number;
    question: string;
}

@Component({
    components: { product, ProductTabs }
})
export default class App extends Vue {
    cart: number[] = [];
    reviews: reviewInterface[] = [];
    details = ['80% cotton', '20% polyester', 'Gender-neutral'];

    increaseCart(id: number) {
        this.cart.push(id);
    }
    decreaseCart(id: number) {
        this.cart = this.cart.filter((_, i) => this.cart.findIndex((el) => el === id) != i);
    }
    /*     addReview(review: string) {
        this.reviews.push(review);
    } */

    mounted() {
        eventBus.$on('add-review', (review: reviewInterface) => this.reviews.push(review));
    }
}
</script>
