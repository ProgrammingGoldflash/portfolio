<script lang="ts" setup>
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome'
import Article from '../classes/Article.vue'
</script>

<template>
    <div id="projects-articles" class="flex flex-col md:flex-row flex-grow h-screen relative h-min">
        <div class="p-2 grid grid-cols-1 gap-4">
            <div v-for="(article, index) in articles" :key="index"
                class="border border-gray-300 rounded p-4 shadow-md flex items-start h-min">
                <!-- <img :src="article.cover_image" alt="article image" class="w-full max-h-20 max-w-xs object-cover mr-4"> -->

                <div class="flex-grow">
                    <div class="flex justify-between items-center">
                        <h2 class="font-bold mt-2">{{ article.title }}</h2>

                        <a :href="article.url" target="_blank" rel="noopener noreferrer"
                            class="bg-blue-500 text-white text-sm font-semibold py-1 px-2 rounded-md">
                            <font-awesome-icon icon="fa-solid fa-newspaper" />
                            Read article
                        </a>
                    </div>

                    <p class="mt-2">{{ article.description }}</p>
                </div>
            </div>
        </div>
    </div>
</template>

<script lang="ts">
export default {
    data() {
        return {
            articles: [] as Article[]
        };
    },
    async mounted() {
        const response = await fetch('https://dev.to/api/articles?username=philip-ainberger');
        const data = await response.json();
        this.articles = data;
    },
};
</script>