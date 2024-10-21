<template>
  <div class="max-w-6xl mx-auto px-4 sm:px-6 lg:px-8 py-12">
    <h1 class="text-3xl font-extrabold text-gray-900 mb-8 text-center">Ukrainian-English Language Learning Table</h1>
    <LanguageTable :words="words" @updateWords="updateWords" />
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'

const words = ref([])

const updateWords = (newWords) => {
  words.value = newWords
}

onMounted(async () => {
  try {
    const response = await fetch('/data/ukrainian-english.json')
    const data = await response.json()
    if (Array.isArray(data)) {
      words.value = data.map((item, index) => ({
        id: index + 1,
        ...item,
        examples: [] // We don't have examples in the JSON, so we'll leave this empty for now
      }))
    } else {
      console.error('Data is not an array:', data)
    }
  } catch (error) {
    console.error('Error fetching or parsing data:', error)
  }
})
</script>