<script lang="ts" setup>
import { ref } from 'vue';

interface Folder {
  id: number;
  name: string;
  children?: Folder[];
}

const props = defineProps<{ folders: Folder[]; selectedFolderId: number | null }>();
const emit = defineEmits<{ (e: 'select', id: number | null): void }>();

const openFolders = ref<Record<number, boolean>>({});

function toggleFolder(folderId: number) {
  openFolders.value[folderId] = !openFolders.value[folderId];
}

function selectFolder(folderId: number) {
  emit('select', folderId === props.selectedFolderId ? null : folderId);
}
</script>

<template>
  <ul class="tree">
    <li v-for="folder in props.folders" :key="folder.id" class="tree__item">
      <div class="tree__block">
        <span
          v-if="folder.children && folder.children.length"
          class="tree__button"
          @click="toggleFolder(folder.id)"
        >
          {{ openFolders[folder.id] ? '-' : '+' }}
        </span>
        <span
          class="tree__name"
          :class="{ tree__selected: folder.id === props.selectedFolderId }"
          @click="selectFolder(folder.id)"
        >
          {{ folder.name }}
        </span>
      </div>

      <FolderTree
        v-if="folder.children && openFolders[folder.id]"
        :folders="folder.children"
        :selectedFolderId="props.selectedFolderId"
        @select="emit('select', $event)"
      />
    </li>
  </ul>
</template>

<style scoped lang="scss">
.tree {
  list-style: none;
  padding-left: 1.5rem;

  &__item {
    margin-bottom: 0.5rem;
  }

  &__block {
    display: flex;
    align-items: center;
    gap: 0.5rem;
  }

  &__selected {
    font-weight: bold;
    background-color: #f0f0f0;
    border-radius: 4px;
    padding: 4px;
  }

  &__button {
    font-weight: bold;
    cursor: pointer;
    user-select: none;
  }

  &__name {
    cursor: pointer;
    padding: 0.2rem 0.4rem;
    border-radius: 4px;

    &:hover {
      background-color: #f0f0f0;
    }
  }
}
</style>
