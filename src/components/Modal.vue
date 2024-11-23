<template>
    <div
        class="fixed inset-0 bg-black bg-opacity-50 flex justify-center items-center"
    >
        <div class="bg-white rounded-lg shadow-lg w-1/2">
            <header class="p-4 border-b">
                <h2 class="text-lg font-semibold">{{ title }}</h2>
            </header>
            <main class="p-4">
                <slot />
            </main>
            <footer class="p-4 border-t flex justify-end gap-2">
                <button @click="onClose" class="bg-gray-200 px-4 py-2 rounded hover:bg-gray-300 transition-colors duration-75">
                    Закрыть
                </button>
                <button
                    @click="onConfirm"
                    class="text-white bg-gradient-to-r from-cyan-500 to-blue-500 hover:bg-gradient-to-bl focus:ring-4 focus:outline-none focus:ring-cyan-300 dark:focus:ring-cyan-800 font-medium rounded-lg text-sm px-4 py-2 text-center"
                >
                    Ок
                </button>
            </footer>
        </div>
    </div>
</template>

<script lang="ts" setup>
import { defineProps, defineEmits } from "vue";

defineProps({
    title: { type: String, required: true },
});

const emit = defineEmits(["close", "select"]);

const onClose = () => emit("close");
const onConfirm = () => emit("select");
</script>
