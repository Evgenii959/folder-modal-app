<script lang="ts" setup>
const props = defineProps<{ title: string }>();
const emit = defineEmits<{ (e: 'close'): void }>();
</script>

<template>
  <div class="modal" @click.self="emit('close')">
    <div class="modal__content">
      <h2 class="modal__title">{{ props.title }}</h2>
      <slot />
      <div class="modal__footer">
        <button class="modal__button" @click="emit('close')">Закрыть</button>
      </div>
    </div>
  </div>
</template>

<style scoped lang="scss">
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
  z-index: 1000;

  &__content {
    background: #ffffff;
    padding: 1.5rem;
    border-radius: 12px;
    max-width: 500px;
    width: 90%;
    box-shadow: 0 4px 10px rgba(0, 0, 0, 0.25);
    animation: fadeIn 0.3s ease-out;

    @keyframes fadeIn {
      from {
        transform: scale(0.9);
        opacity: 0;
      }
      to {
        transform: scale(1);
        opacity: 1;
      }
    }
  }

  &__title {
    font-size: 1.5rem;
    font-weight: 600;
    color: #333333;
    margin-bottom: 1rem;
    text-align: center;
  }

  &__footer {
    display: flex;
    justify-content: flex-end;
    margin-top: 1rem;
  }

  &__button {
    background-color: #ff5c5c;
    color: #ffffff;
    border: none;
    border-radius: 6px;
    padding: 0.5rem 1rem;
    font-size: 0.9rem;
    cursor: pointer;
    transition: background-color 0.3s;

    &:hover {
      background-color: #ff3838;
    }

    &:active {
      background-color: #e33232;
    }
  }
}
</style>
