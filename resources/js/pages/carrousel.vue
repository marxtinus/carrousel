<script setup lang="ts">
import { Carousel, Slide, Pagination, Navigation } from 'vue3-carousel';
import 'vue3-carousel/dist/carousel.css';

const carouselConfig = {
    itemsToShow: 2.5,
    wrapAround: true,
};
</script>

<template>
    <Carousel v-bind="carouselConfig">
        <Slide v-for="slide in 10" :key="slide">
            <div class="carousel__item">{{ slide }}</div>
        </Slide>

        <template #addons>
            <Navigation />
            <Pagination />
        </template>
    </Carousel>
</template>

<style scoped></style>
