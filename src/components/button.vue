<script setup>
import { ref } from 'vue';
import Modal from './Modal.vue';

const emits = defineEmits(['ok']);
const props = defineProps(['text']);

const showModal = ref(false);

function send() {
  showModal.value = true;
  emits('ok', 'hello');
}

function closeModal() {
  showModal.value = false;
}
</script>

<template>
  <div class="button-container">
    <div class="button" @click="send">
      {{ props.text }}
    </div>
    <Modal :visible="showModal" message="并没有什么用!这是一个VUE组件" @close="closeModal" />
  </div>
</template>

<style scoped>
.button-container {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100%;
}

.button {
  width: 50px;
  height: 30px;
  line-height: 30px;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
  background-color: rgb(224, 193, 193);
  border-radius: 8px;
  cursor: pointer;
  user-select: none;
}
</style>
