<template>
    <Transition name="modal-outer" :duration="{ enter: 500, leave: 800 }">
        <div v-show="modalActive"
            class="absolute w-full bg-black bg-opacity-30 h-screen top-0 left-0 flex justify-center px-8">
            <Transition name="modal-inner">
                <div v-if="modalActive" class="p-4 bg-white self-start mt-32 max-w-screen-md">
                    <slot />

                    <button class="text-white mt-8 bg-primary py-2 px-6" @click="$emit('close-modal')">
                        Close
                    </button>
                </div>
            </Transition>

        </div>
    </Transition>
</template>

<script setup lang="ts">
defineEmits(['close-modal'])
defineProps({
    modalActive: {
        type: Boolean,
        default: false,
    }
})
</script>

<style scoped>
.modal-outer-enter-active {
    animation: bounce-in 0.5s;
}

.modal-outer-leave-active {
    animation: bounce-in 0.5s reverse;
}

@keyframes bounce-in {
    0% {
        transform: scale(0);
    }

    50% {
        transform: scale(1.25);
    }

    100% {
        transform: scale(1);
    }
}
</style>