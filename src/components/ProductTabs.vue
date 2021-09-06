<template lang="pug">
.tabs-container
    span.tab(
        v-for='(tab, index) in tabs',
        :key='index',
        @click='selected = tab',
        :class='{ activeTab: selected === tab }'
    ) {{ tab }}
    ReviewList(v-show='selected === tabs[0]', :reviews='reviews')
    ProductReview(v-show='selected === tabs[1]')
    ProductShipping(v-show='selected === tabs[2]')
    Details(v-show='selected===tabs[3]', :details='details')
</template>

<script lang="ts">
import Vue from 'vue';
import { Component, Prop } from 'vue-property-decorator';

import ProductReview from '@/components/ProductReview.vue';
import ReviewList from '@/components/ReviewList.vue';
import Details from '@/components/Details.vue';
import ProductShipping from '@/components/ProductShipping.vue';
import { reviewInterface } from '@/App.vue';

@Component({
    components: { ProductReview, ReviewList, Details, ProductShipping }
})
export default class ProductTabs extends Vue {
    @Prop({
        required: true,
        type: Array
    })
    reviews!: reviewInterface[];

    @Prop({
        required: true,
        type: Boolean
    })
    premium!: boolean;

    @Prop({
        required: true,
        type: Array
    })
    details!: string[];

    tabs: string[] = ['Reviews', 'Make a Review', 'Shipping', 'Details'];
    selected: string = this.tabs[0];
}
</script>

<style scoped>
.activeTab {
    font-weight: bold;
    color: blue;
}
.tab {
    text-decoration: underline;
}
.tabs-container span {
    margin: 10px;
}
</style>
