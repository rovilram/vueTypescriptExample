<template lang="pug">
.shipping-container
    h2 Shipping
    p {{ shipping }}
</template>

<script lang="ts">
import Vue from 'vue';
import { Component, Prop } from 'vue-property-decorator';

@Component
export default class ProductShipping extends Vue {
    @Prop({
        required: true,
        type: Boolean
    })
    premium!: boolean;

    get shipping() {
        return !this.premium ? '3,00 €' : 'Eres Premium, es GRATIS!!!';
    }
}
</script>