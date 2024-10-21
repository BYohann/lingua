<template>
  <div>
    <div class="mb-4 flex justify-end">
      <button @click="openModal" class="bg-green-500 hover:bg-green-600 text-white font-bold py-2 px-4 rounded-full transition duration-300 ease-in-out transform hover:-translate-y-1 hover:scale-110">
        Add Word
      </button>
    </div>
    <div class="overflow-x-auto shadow-lg rounded-lg">
      <table class="min-w-full bg-white">
        <thead>
          <tr>
            <th v-for="header in headers" :key="header" @click="sort(header.toLowerCase())" class="px-6 py-3 border-b border-gray-200 bg-gray-50 text-left text-xs leading-4 font-medium text-gray-500 uppercase tracking-wider cursor-pointer">
              {{ header }}
              <span v-if="sortColumn === header.toLowerCase()">{{ sortDirection === 'asc' ? '▲' : '▼' }}</span>
            </th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="word in sortedWords" :key="word.id" class="hover:bg-gray-100">
            <td class="px-6 py-4 whitespace-no-wrap border-b border-gray-200">
              {{ word.english }}
            </td>
            <td class="px-6 py-4 whitespace-no-wrap border-b border-gray-200">
              {{ word.ukrainian }}
            </td>
            <td class="px-6 py-4 whitespace-no-wrap border-b border-gray-200">
              {{ word.tag }}
            </td>
            <td class="px-6 py-4 border-b border-gray-200">
              <ul>
                <li v-for="example in word.examples" :key="example.id" class="mb-1">
                  {{ example.sentence }}
                </li>
              </ul>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
    <AddTermModal :isOpen="isModalOpen" @close="closeModal" @addTerm="addNewTerm" />
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'
import AddTermModal from './AddTermModal.vue'

const props = defineProps({
  words: {
    type: Array,
    required: true
  }
})

const emit = defineEmits(['updateWords'])

const headers = ['English', 'Ukrainian', 'Tag', 'Examples']

const sortColumn = ref('english')
const sortDirection = ref('asc')
const isModalOpen = ref(false)

const sort = (column) => {
  if (sortColumn.value === column) {
    sortDirection.value = sortDirection.value === 'asc' ? 'desc' : 'asc'
  } else {
    sortColumn.value = column
    sortDirection.value = 'asc'
  }
}

const sortedWords = computed(() => {
  return [...props.words].sort((a, b) => {
    let compareA = a[sortColumn.value]
    let compareB = b[sortColumn.value]

    if (sortColumn.value === 'examples') {
      compareA = a.examples ? a.examples.length : 0
      compareB = b.examples ? b.examples.length : 0
    }

    if (compareA < compareB) return sortDirection.value === 'asc' ? -1 : 1
    if (compareA > compareB) return sortDirection.value === 'asc' ? 1 : -1
    return 0
  })
})

const openModal = () => {
  isModalOpen.value = true
}

const closeModal = () => {
  isModalOpen.value = false
}

const addNewTerm = (newTerm) => {
  emit('updateWords', [...props.words, newTerm])
}
</script>