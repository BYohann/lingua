<template>
  <div v-if="isOpen" class="fixed inset-0 bg-gray-600 bg-opacity-50 overflow-y-auto h-full w-full flex items-center justify-center">
    <div class="bg-white p-8 rounded-lg shadow-xl w-full max-w-md">
      <h2 class="text-2xl font-bold mb-4">Add New Word</h2>
      <form @submit.prevent="addTerm">
        <div class="mb-4">
          <label for="english" class="block text-sm font-medium text-gray-700">English</label>
          <input type="text" id="english" v-model="newTerm.english" required class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-blue-300 focus:ring focus:ring-blue-200 focus:ring-opacity-50">
        </div>
        <div class="mb-4">
          <label for="ukrainian" class="block text-sm font-medium text-gray-700">Ukrainian</label>
          <input type="text" id="ukrainian" v-model="newTerm.ukrainian" required class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-blue-300 focus:ring focus:ring-blue-200 focus:ring-opacity-50">
        </div>
        <div class="mb-4">
          <label for="tag" class="block text-sm font-medium text-gray-700">Tag</label>
          <input type="text" id="tag" v-model="newTerm.tag" required class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-blue-300 focus:ring focus:ring-blue-200 focus:ring-opacity-50">
        </div>
        <div class="mb-4">
          <label for="example" class="block text-sm font-medium text-gray-700">Example</label>
          <input type="text" id="example" v-model="newTerm.example" class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-blue-300 focus:ring focus:ring-blue-200 focus:ring-opacity-50">
        </div>
        <div class="flex justify-end">
          <button type="button" @click="closeModal" class="mr-2 px-4 py-2 text-sm font-medium text-gray-700 bg-gray-100 rounded-md hover:bg-gray-200 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-gray-500">Cancel</button>
          <button type="submit" class="px-4 py-2 text-sm font-medium text-white bg-blue-600 rounded-md hover:bg-blue-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-blue-500">Add Word</button>
        </div>
      </form>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const props = defineProps({
  isOpen: Boolean
})

const emit = defineEmits(['close', 'addTerm'])

const newTerm = ref({
  english: '',
  ukrainian: '',
  tag: '',
  example: ''
})

const addTerm = () => {
  const termToAdd = {
    ...newTerm.value,
    id: Date.now(),
    examples: newTerm.value.example ? [{ id: Date.now(), sentence: newTerm.value.example }] : []
  }
  emit('addTerm', termToAdd)
  newTerm.value = { english: '', ukrainian: '', tag: '', example: '' }
  closeModal()
}

const closeModal = () => {
  emit('close')
}
</script>