<template>
    <main class="container text-white">
        <div class="pt-4 mb-8 relative">
            <input v-model="searchQuery" type="text" @input="getSearchResults" placeholder="Search a City or State"
                class="py-2 px-1 w-full bg-transparent border-b focus:border-secondary focus:outline-none focus:shadow-[0px_1px_0_0_#004EE7]" />

            <ul class="absolute bg-secondary text-wrap w-full shadow-md py-2 px-1 top-[66px]" v-if="mapboxSearcResults">
                <li v-for="searchResult in mapboxSearcResults" :key="searchResult.id" class="py-2 cursor-pointer">
                    {{ searchResult.place_name }}
                </li>
            </ul>
            <div class="" v-else></div>
        </div>
    </main>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import axios from 'axios'

const queryTimeout = ref(null)
const searchQuery = ref("")
const access_token = "pk.eyJ1IjoibWFpbWFsZWUiLCJhIjoiY2x2eDBpejF2MG5uOTJqb2c3emp3emJtbyJ9.A8yoif0XGvMssyOE0udqDg"
const mapboxSearcResults = ref(null)

const getSearchResults = function () {
    clearTimeout(queryTimeout.value)
    queryTimeout.value = setTimeout(async () => {
        if (searchQuery.value !== "") {
            try {
                const result = await axios.get(`https://api.mapbox.com/geocoding/v5/mapbox.places/${searchQuery.value}.json?access_token=${access_token}`);
                mapboxSearcResults.value = result.data.features
                console.log(mapboxSearcResults.value, "rsults")
            } catch (error) {
                console.error("Error fetching search results:", error)
            }
        } else {
            mapboxSearcResults.value = null
        }
    }, 300)
}
</script>
