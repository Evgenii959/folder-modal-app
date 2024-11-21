<script lang="ts" setup>
import { ref } from 'vue';
import Modal from './Modal.vue';
import FolderTree from './FolderTree.vue';
import { mockFolders } from '../mock/mockFolders';

const isModalOpen = ref(false);
const selectedFolder = ref<number | null>(null);

function openModal() {
  isModalOpen.value = true;
}

function closeModal() {
  isModalOpen.value = false;
}

function handleSelect(id: number) {
  selectedFolder.value = id;
}
</script>

<template>
  <button @click="openModal">Открыть</button>
  <Modal v-if="isModalOpen" title="Выберите папку" @close="closeModal">
    <FolderTree :folders="mockFolders" @select="handleSelect" />
    <button @click="closeModal">Ок</button>
  </Modal>
  <p>Выбранная папка: {{ selectedFolder }}</p>
</template>