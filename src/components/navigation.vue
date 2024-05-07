<template>
    <header class="sticky top-0 bg-primary shadow-lg">
        <nav class="container flex sm:flex-row md:items-center items-center gap-2 py-5 text-white">
            <RouterLink :to="{ name: 'home' }">
                <div class="flex items-center gap-5 flex-1">
                    <i class="fa-solid fa-sun text-2xl"></i>
                    <p class="text-2xl  sm:text-sm md:text-2xl md:italic">Weather App</p>
                </div>
            </RouterLink>

            <div class="flex gap-5 flex-1 justify-end">
                <i class="fa-solid fa-circle-info text-xl hover:text-secondary duration-150 cursor-pointer"
                    @click="toggleModal"></i>
                <i class="fa-solid fa-plus-circle text-xl hover:text-secondary duration-150 cursor-pointer"></i>
            </div>

            <BaseModal :modalActive="modalActive" @close-modal="toggleModal">
                <div class="text-black">
                    Hell
                </div>
            </BaseModal>
        </nav>
    </header>
</template>

<script setup lang="ts">
import { RouterLink } from 'vue-router'
import { ref } from 'vue'
import BaseModal from "./BaseModal.vue"

const modalActive = ref(null)
const toggleModal = () => {
    modalActive.value = !modalActive.value
}
</script>
