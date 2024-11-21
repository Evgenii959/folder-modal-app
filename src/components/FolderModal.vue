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

function handleSelect(id: number | null) {
  selectedFolder.value = id;
}
</script>

<template>
  <div class="main">
    <button class="main__button" @click="openModal">Открыть</button>
    <Modal v-if="isModalOpen" title="Выберите папку" @close="closeModal">
      <FolderTree 
        :folders="mockFolders" 
        :selectedFolderId="selectedFolder" 
        @select="handleSelect" 
      />
      <div class="main__footer">
        <button class="main__button" @click="closeModal">Ок</button>
      </div>
    </Modal>
    <p class="main__selected">Выбранная папка: {{ selectedFolder }}</p>
  </div>
</template>

<style scoped lang="scss">
.main {
  padding: 2rem;
  text-align: center;

  &__button {
    background-color: #4caf50;
    color: white;
    border: none;
    border-radius: 4px;
    padding: 0.5rem 1.2rem;
    font-size: 1rem;
    cursor: pointer;
    transition: background-color 0.3s;

    &:hover {
      background-color: #45a049;
    }

    &:active {
      background-color: #3e8e41;
    }
  }

  &__selected {
    margin-top: 1rem;
    font-size: 1.5rem;
    color: #555;

    span {
      font-weight: bold;
    }
  }

  &__footer {
    margin-top: 1rem;
    text-align: right;

    &__button {
      background-color: #007bff;
      color: white;
      border: none;
      border-radius: 4px;
      padding: 0.5rem 1rem;
      font-size: 0.9rem;
      cursor: pointer;
      transition: background-color 0.3s;

      &:hover {
        background-color: #0056b3;
      }

      &:active {
        background-color: #004099;
      }
    }
  }
}
</style>
