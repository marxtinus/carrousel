<script setup lang="ts">
import { ref } from 'vue';
import { Carousel, Slide, Navigation } from 'vue3-carousel';
import 'vue3-carousel/dist/carousel.css';

const currentSlide = ref(0);
const slideTo = (nextSlide: number) => (currentSlide.value = nextSlide);

const galleryConfig = {
    itemsToShow: 1,
    wrapAround: true,
    slideEffect: 'fade',
    mouseDrag: false,
    touchDrag: false,
    height: 620,
};
const thumbnailsConfig = {
    height: 80,
    itemsToShow: 6,
    wrapAround: true,
    touchDrag: false,
    gap: 10,
};

const images = [
    {
        src: '/storage/img/1.png',
        description:
            'Page dynamique où les usagers voient leur tâche classées par priorité avec un indicateur sur la carte selectionnable',
    },
    {
        src: '/storage/img/2.png',
        description:
            "Différents graphiques des status dans des employées dans l'application.",
    },
    {
        src: '/storage/img/3.png',
        description:
            "Authentification de l'usager un utilisant son numero corporatif tiré du GAL Entra ID (obtenus par graph API).",
    },
    {
        src: '/storage/img/4.png',
        description:
            'Exemple de tableau de board à l\'usage de décideurs',
    },
    {
        src: '/storage/img/5.png',
        description: 'Interface Mass mailing pour créer le couriel',
    },
    {
        src: '/storage/img/6.png',
        description: 'Exemple de couriel formatté entreprise.',
    },
];
</script>

<template>
    <div class="flex min-h-screen items-center justify-center bg-gray-800">
        <div class="flex w-270 flex-none flex-col gap-5">
            <p class="text-center text-lg text-white">
                {{ images[currentSlide]?.description }}
            </p>
            <Carousel
                id="gallery"
                v-bind="galleryConfig"
                v-model="currentSlide"
            >
                <Slide v-for="(image, index) in images" :key="index">
                    <img
                        :src="image.src"
                        alt="Gallery Image"
                        class="gallery-image"
                    />
                </Slide>
            </Carousel>

            <Carousel
                id="thumbnails"
                v-bind="thumbnailsConfig"
                v-model="currentSlide"
            >
                <Slide v-for="(image, index) in images" :key="index">
                    <template #default="{ currentIndex, isActive }">
                        <div
                            :class="['thumbnail', { 'is-active': isActive }]"
                            @click="slideTo(currentIndex)"
                        >
                            <img
                                :src="image.src"
                                alt="Thumbnail Image"
                                class="thumbnail-image"
                            />
                        </div>
                    </template>
                </Slide>

                <template #addons>
                    <Navigation />
                </template>
            </Carousel>
        </div>
    </div>
</template>

<style>
:root {
    background-color: #242424;
}



img {
    border-radius: 8px;
    width: 100%;
    height: 100%;
    object-fit: cover;
}

.gallery-image {
    border-radius: 16px;
}

#thumbnails {
    margin-top: 10px;
}

.thumbnail {
    height: 100%;
    width: 100%;
    cursor: pointer;
    opacity: 0.6;
    transition: opacity 0.3s ease-in-out;
}

.thumbnail:hover {
    opacity: 1;
}
</style>
