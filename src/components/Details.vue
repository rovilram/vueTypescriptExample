<template lang="pug">
.detail-container
    h2 Details
    ul
        li(v-for='detail in details') {{ detail }}
</template>

<script lang="ts">
import Vue from 'vue';
import { Prop, Component } from 'vue-property-decorator';

@Component
export default class Details extends Vue {
    @Prop({
        type: Array,
        required: true,
        default: []
    })
    details!: string[];
}
</script>
I
