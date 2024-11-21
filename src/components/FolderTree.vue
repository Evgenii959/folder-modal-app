<script lang="ts" setup>
import { ref } from 'vue';

interface Folder {
  id: number;
  name: string;
  children: Folder[];
}

defineProps<{ folders: Folder[] }>();
const emit = defineEmits<{ (e: 'select', id: number): void }>();

const openNodes = ref<Set<number>>(new Set());
const selectedFolder = ref<number | null>(null);

function toggleNode(id: number) {
  if (openNodes.value.has(id)) {
    openNodes.value.delete(id);
  } else {
    openNodes.value.add(id);
  }
}

function toggleSelection(id: number) {
  selectedFolder.value = id;
  emit('select', id);
}

function isOpen(id: number) {
  return openNodes.value.has(id);
}
</script>

<template>
  <ul>
    <li v-for="folder in folders" :key="folder.id">
      <div class="folder">
        <span v-if="folder.children.length" class="folder__button" @click="toggleNode(folder.id)">
          {{ isOpen(folder.id) ? '-' : '+' }}
        </span>
        <span @click="toggleSelection(folder.id)" :class="{ selected: selectedFolder === folder.id }">
          {{ folder.name }}
        </span>
      </div>
      <FolderTree
        v-if="folder.children.length && isOpen(folder.id)"
        :folders="folder.children"
        @select="emit('select', $event)"
      />
    </li>
  </ul>
</template>

<style scoped>
.folder {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  cursor: pointer;
}

.folder__button {
  font-weight: bold;
  user-select: none;
}
</style>