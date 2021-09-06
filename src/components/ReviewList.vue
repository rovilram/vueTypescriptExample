<template lang="pug">
.reviews-container
    h2 Reviews
    div(v-if='!reviews.length') There are no reviews
    ul
        li(v-for='{ name, review, rating, question } in reviews')
            p Nombre: {{ name }}
            p Reseña: {{ review }}
            p Nota: {{ rating }}
            p Respuesta: {{ question }}
</template>

<script lang="ts">
import { reviewInterface } from '@/App.vue';
import Vue from 'vue';
import { Component, Prop } from 'vue-property-decorator';

@Component
export default class ReviewList extends Vue {
    @Prop({
        type: Array,
        required: true,
        default: []
    })
    reviews!: reviewInterface[];
}
</script>

