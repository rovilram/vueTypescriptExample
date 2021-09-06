<template lang="pug">
.addReview-container
    h2 Add a review

    p(v-if='errors.length') Please correct the folowing errors
        ul
            li(v-for='error in errors') {{ error }}

    form.review-form(@submit.prevent='onSubmit')
        p
            label(for='name') Name:
            input#name(v-model='name', placeholder='name')
        p
            label(for='review') Review:
            textarea#review(v-model='review')
        p
            label(for='rating') Rating:
            select#rating(v-model.number='rating')
                option 5
                option 4
                option 3
                option 2
                option 1
        p
            label(for='question') Would you recommend this product?
            div
            input#question-yes(type='radio', name='question', value='yes', v-model='question')
            label(for='question-yes') Yes
            div
            input#question-no(type='radio', name='question', value='no', v-model='question')
            label(for='question-no') No
            div
        p
            input(type='submit', value='Submit')
</template>

<script lang="ts">
import { reviewInterface } from '@/App.vue';
import Vue from 'vue';
import Component from 'vue-class-component';
import eventBus from './eventBus';
@Component
export default class ProductReview extends Vue {
    name = '';
    review = '';
    rating = 0;
    question = '';
    errors: string[] = [];
    onSubmit() {
        if (this.name && this.review && this.rating) {
            const review: reviewInterface = {
                name: this.name,
                review: this.review,
                rating: this.rating,
                question: this.question
            };
            eventBus.$emit('add-review', review);
            this.name = '';
            this.review = '';
            this.rating = 0;
            this.question = '';
        } else {
            if (!this.name) this.errors.push('Name required');
            if (!this.review) this.errors.push('Review required');
            if (!this.rating) this.errors.push('RatingI required');
            !this.question && this.errors.push('Review question required');
        }
    }
}
</script>
