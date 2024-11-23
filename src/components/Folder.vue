<script lang="ts" setup>
import { defineProps, defineEmits } from "vue";
import { ref } from "vue";

interface FolderType {
    id: number;
    name: string;
    children: FolderType[];
}

defineProps({
    folders: {
        type: Array as () => FolderType[],
        required: true,
    },
});

const emit = defineEmits(["select"]);

const selectedFolderId = ref<number | null>(null);
const openFolders = ref<Set<number>>(new Set());

const toggle = (folderId: number) => {
    if (openFolders.value.has(folderId)) {
        openFolders.value.delete(folderId);
    } else {
        openFolders.value.add(folderId);
    }
};

const isOpen = (folderId: number) => openFolders.value.has(folderId);

const handleSelect = (folderId: number) => {
    selectedFolderId.value = folderId;
    emit("select", folderId);
};
</script>

<template>
    <div>
        <div
            v-for="folder in folders"
            :key="folder.id"
            class="flex flex-col pl-4"
        >
            <div
                @click="toggle(folder.id)"
                :class="[
                    'cursor-pointer',
                    selectedFolderId === folder.id
                        ? 'font-semibold text-blue-600'
                        : 'font-normal',
                    folder.children.length > 0 ? 'font-bold' : 'font-normal',
                    'hover:bg-gray-200 rounded p-2',
                ]"
            >
                {{ folder.name }}
            </div>
            <div
                v-if="folder.children.length && isOpen(folder.id)"
                class="pl-6"
            >
                <Folder :folders="folder.children" @select="handleSelect" />
            </div>
        </div>
    </div>
</template>
