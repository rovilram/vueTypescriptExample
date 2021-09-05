<template lang="pug">
.product
    .product-image
        img.calcetin(:src='getImage')

    .product-info
        h1 {{ title }}

        p Shipping: {{ shipping }}

        p Enlace:
            a(target='_blank', :href='link') LINK

        p(v-if='inStock') In stock

        p(v-else='', :class='{ outOfStock: !inStock }') Out of stock

        span(v-if='onSale') {{ onSaletext }}

        Details(:details='details')

        .variant-container
            .variant-box(
                v-for='(variant, index) in variants',
                :key='variant.variantId',
                :style='{ backgroundColor: backgroundColor(variant.variantColor) }',
                @mouseover='chooseVariant(index)'
            )
                | {{ variant.variantColor }}
        .sizes-container
            h2 Sizes
            ul
                li(v-for='size in sizes') {{ size }}

        button(v-on:click='addToCart', :disabled='!inStock', :class='{ disabledButton: !inStock }') Add to Cart

        button(v-on:click='removeFromCart') Remove from Cart
</template>

<script lang="ts">
import Vue from 'vue';
import { Component, Prop } from 'vue-property-decorator';
import Details from './Details.vue';
@Component({
    components: { Details }
})
export default class product extends Vue {
    @Prop({
        type: Boolean,
        required: true
    })
    premium!: string;

    product = 'Socks';

    image = '@/public/assets/patitos.jpg';

    selectedVariant = 0;

    link = 'https://www.google.com/search?q=olakase';

    inventory = 11;

    onSale = true;

    details = ['80% cotton', '20% polyester', 'Gender-neutral'];

    variants = [
        {
            variantId: 1,
            variantColor: 'patitos',
            image: '../assets/patitos.jpg',
            variantQuantity: 10
        },
        {
            variantId: 2,
            variantColor: 'rallitas',
            image: '../assets/rallitas.jpg',
            variantQuantity: 10
        }
    ];

    sizes = [38, 40, 42, 44, 46];

    brand = 'calcetolandia';

    addToCart() {
        this.$emit('add-to-card', this.variants[this.selectedVariant].variantId);
    }

    removeFromCart() {
        this.$emit('remove-from-card', this.variants[this.selectedVariant].variantId);
    }

    chooseVariant(index: number) {
        this.selectedVariant = index;
    }

    backgroundColor(color: string) {
        console.log(color);
        return color === 'patitos' ? 'yellow' : 'red';
    }

    get title() {
        return `${this.brand} - ${this.product}`;
    }
    get onSaletext() {
        return `${this.brand} - ${this.product} - ON SALE`;
    }
    get getImage() {
        return this.variants[this.selectedVariant].image;
    }
    get inStock() {
        return this.variants[this.selectedVariant].variantQuantity;
    }
    get shipping() {
        return !this.premium ? '3,00 €' : 'Eres Premium, es GRATIS!!!';
    }
}
</script>
