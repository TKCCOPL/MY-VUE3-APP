<template>
  <div class="modal-overlay" v-if="visible">
    <div class="modal-content">
      <p>{{ message }}</p>
      <button style="border-radius: 10px;" @click="close">确定</button>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const props = defineProps({
  visible: Boolean,
  message: String,
});

const emits = defineEmits(['close']);

function close() {
  emits('close');
}
</script>

<style scoped>
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
  border-radius: 10px;
}

.modal-content {
  background: white;
  padding: 20px;
  border-radius: 10px;
  text-align: center;
  
}
</style>