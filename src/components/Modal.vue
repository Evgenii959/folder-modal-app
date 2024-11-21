<script lang="ts" setup>
defineProps<{ title: string }>();
const emit = defineEmits<{ (e: 'close'): void }>();
</script>

<template>
  <div class="modal" @click.self="emit('close')">
    <div class="modal__content">
      <h2>{{ title }}</h2>
      <slot />
      <div class="modal__footer">
        <button @click="emit('close')">Закрыть</button>
      </div>
    </div>
  </div>
</template>

<style scoped>
.modal {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
}
.modal__content {
  background: white;
  padding: 1rem;
  border-radius: 8px;
  max-width: 500px;
  width: 100%;
}
</style>