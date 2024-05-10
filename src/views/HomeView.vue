<template>
    <main class="container text-white">
        <div class="pt-4 mb-8 relative">
            <input v-model="searchQuery" type="text" @input="getSearchResults" placeholder="Search a City or State"
                class="py-2 px-1 w-full bg-transparent border-b focus:border-secondary focus:outline-none focus:shadow-[0px_1px_0_0_#004EE7]" />

            <ul class="absolute bg-secondary text-wrap w-full shadow-md py-2 px-1 top-[66px]" v-if="mapboxSearcResults">
                <p v-if="searchError">
                    Sorry, something went wrong, pls try again!
                </p>
                <p v-if="!serverError && mapboxSearcResults.length === 0">
                    No result for your query, try again next.
                </p>
                <template v-else>
                    <li v-for="searchResult in mapboxSearcResults" :key="searchResult.id" class="py-2 cursor-pointer"
                        @click="previewCity(searchResult)">
                        {{ searchResult.place_name }}
                    </li>
                </template>
            </ul>

        </div>
    </main>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import axios from 'axios'
import { useRouter } from 'vue-router'
const router = useRouter()


const previewCity = (searchResult) => {
    console.log(searchResult)
    const [city, state] = searchResult.place_name.split(',')
    router.push({
        name: "CityView",
        params: { state: state ? state.trim().replaceAll(" ", "") : "", city: city ? city.trim() : "" }, // Check if state and city are defined before using trim()
        query: {
            lat: searchResult.geometry.coordinates[1],
            lng: searchResult.geometry.coordinates[0],
            preview: true,
        },
    })
}

const queryTimeout = ref(null)
const searchQuery = ref("")
const access_token = "pk.eyJ1IjoibWFpbWFsZWUiLCJhIjoiY2x2eDBpejF2MG5uOTJqb2c3emp3emJtbyJ9.A8yoif0XGvMssyOE0udqDg"
const mapboxSearcResults = ref(null)
const searchError = ref(null)

const getSearchResults = function () {
    clearTimeout(queryTimeout.value)
    queryTimeout.value = setTimeout(async () => {
        if (searchQuery.value !== "") {
            try {
                const result = await axios.get(`https://api.mapbox.com/geocoding/v5/mapbox.places/${searchQuery.value}.json?access_token=${access_token}`);
                mapboxSearcResults.value = result.data.features
                console.log(mapboxSearcResults.value, "rsults")
            } catch {
                searchError.value = true
            }
        } else {
            mapboxSearcResults.value = null
        }
    }, 300)
}
</script>
