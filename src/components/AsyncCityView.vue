<template>
    <div>

    </div>
</template>

<script setup lang="ts">
import axios from 'axios'
import { useRoute } from "vue-router"

const router = useRoute()
const getWeatherData = async () => {
    try {
        const weatherData = await axios.get(`https://api.openweathermap.org/data/3.0/onecall?lat=${router.query.lat}&lon=${router.query.lng}&exclude={part}&appid=f2a0eace87ba1251e9c026af9b68c97&units=imperial`)
        // call curent date and time 
        const localOffset = new Date().getTimezoneOffset() * 60000;
        const utc = weatherData.data.current.dt * 1000 + localOffset
        weatherData.data.currentTime = utc + 1000 * weatherData.data.timezone_offset;

        // call hourly weather offset 
        weatherData.data.hourly.forEach((hour) => {
            const utc = hour.dt * 1000 + localOffset
            hour.currentTime = utc + 1000 * weatherData.data.timezone_offset
        })

        return weatherData
    } catch (err) {
        console.log(err)
    }
}
const fetchWeatherData = async () => {
    const weatherData = await getWeatherData()
    console.log(weatherData, "Weather Data")
    console.log("Hello")
}

fetchWeatherData()

console.log("Hello")
</script>
