<template>
    <header class="sticky top-0 bg-primary shadow-lg">
        <nav class="container flex sm:flex-row md:items-center items-center gap-2 py-5 text-white">
            <RouterLink :to="{ name: 'home' }">
                <div class="flex items-center gap-5 flex-1">
                    <i class="fa-solid fa-sun md:text-2xl"></i>
                    <p class="text-sm md:text-xl">Maimalee Weather App</p>
                </div>
            </RouterLink>
            <div class="flex gap-5 flex-1 justify-end">
                <i class="fa-solid fa-circle-info text-xl hover:text-secondary duration-150 cursor-pointer"
                    @click="toggleModal"></i>
                <i class="fa-solid fa-plus-circle text-xl hover:text-secondary duration-150 cursor-pointer"></i>
            </div>

            <BaseModal :modalActive="modalActive" @close-modal="toggleModal">
                <div class="text-black">
                    <p class="md:text-2xl">About:</p>
                    <p class="text-xs mt-4 md:text-lg">Lorem, ipsum dolor sit amet consectetur adipisicing elit. Nisi,
                        eligendi
                        repellendus? Temporibus,
                        esse!</p>

                    <p class="md:text-2xl mt-4 text-bold">How It Works</p>
                    <ul class="mt-4 text-xs md:text-lg">
                        <li>Lorem ipsum dolor sit amet consectetur adipisicing.</li>
                        <li>Lorem ipsum dolor sit amet consectetur adipisicing.</li>
                        <li>Lorem ipsum dolor sit amet consectetur adipisicing.</li>
                    </ul>

                    <p class=" mt-4 mb-4 md:text-2xl text-justify">Removing a City</p>
                    <p class="text-xs md:text-lg">Lorem ipsum dolor sit amet, consectetur adipisicing elit. Earum,
                        exercitationem eaque numquam
                        dolorum quisquam doloremque dolore. Neque fugiat quidem ipsam!</p>
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
