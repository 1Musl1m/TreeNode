<script lang="ts" setup>
import { ref } from "vue";
import Modal from "./components/Modal.vue";
import Folder from "./components/Folder.vue";

const isModalOpen = ref(false);
const mockFolders = ref([
    {
        id: 1,
        name: "Папка 1",
        children: [
            { id: 2, name: "Папка 1.1", children: [] },
            {
                id: 3,
                name: "Папка 1.2",
                children: [{ id: 4, name: "Папка 1.2.1", children: [] }],
            },
        ],
    },
    { id: 5, name: "Папка 2", children: [] },
]);

const selectedFolder = ref<number | null>(null);

const openModal = () => {
    isModalOpen.value = true;
};
const closeModal = () => {
    isModalOpen.value = false;
};
const handleSelect = (folderId: number) => {
    selectedFolder.value = folderId;
    closeModal();
};
</script>

<template>
    <div
        class="flex flex-col items-center justify-center min-h-screen bg-gray-100"
    >
        <button
            @click="openModal"
            type="button"
            class="text-white bg-gradient-to-br from-purple-600 to-blue-500 hover:bg-gradient-to-bl focus:ring-4 focus:outline-none focus:ring-blue-300 dark:focus:ring-blue-800 font-medium rounded-lg text-sm px-5 py-2.5 text-center me-2 mb-2"
        >
            Открыть
        </button>
        <Modal
            v-if="isModalOpen"
            :title="'Выберите папку'"
            @close="closeModal"
            @select="handleSelect"
        >
            <Folder :folders="mockFolders" @select="handleSelect" />
        </Modal>
    </div>
</template>
