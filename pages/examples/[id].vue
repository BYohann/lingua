<template>
  <div class="max-w-4xl mx-auto px-4 sm:px-6 lg:px-8 py-12">
    <h1 class="text-3xl font-extrabold text-gray-900 mb-8 text-center">Examples for "{{ word.term }}"</h1>
    <div class="bg-white shadow overflow-hidden sm:rounded-lg">
      <div class="px-4 py-5 sm:px-6">
        <h2 class="text-lg leading-6 font-medium text-gray-900">Example Sentences</h2>
        <p class="mt-1 max-w-2xl text-sm text-gray-500">Practice using "{{ word.term }}" in context.</p>
      </div>
      <div class="border-t border-gray-200">
        <ul class="divide-y divide-gray-200">
          <li v-for="example in word.examples" :key="example.id" class="px-4 py-4 sm:px-6">
            <p class="text-sm font-medium text-gray-900">{{ example.sentence }}</p>
          </li>
        </ul>
      </div>
    </div>
    <div class="mt-8 text-center">
      <NuxtLink to="/" class="inline-flex items-center px-6 py-3 border border-transparent text-base font-medium rounded-full shadow-sm text-white bg-blue-600 hover:bg-blue-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-blue-500 transition duration-300 ease-in-out transform hover:-translate-y-1 hover:scale-110">
        Back to Table
      </NuxtLink>
    </div>
  </div>
</template>

<script setup>
import { useRoute } from 'vue-router'
import { computed } from 'vue'

const route = useRoute()
const words = [
  {
    id: 1,
    term: 'Bonjour',
    definition: 'Hello',
    root: 'Old French "bon jor" (good day)',
    examples: [
      { id: 1, sentence: 'Bonjour, comment allez-vous?' },
      { id: 2, sentence: 'Je dis bonjour à mes voisins chaque matin.' }
    ]
  },
  {
    id: 2,
    term: 'Merci',
    definition: 'Thank you',
    root: 'Old French "merci" (reward, favor)',
    examples: [
      { id: 3, sentence: 'Merci beaucoup pour votre aide.' },
      { id: 4, sentence: 'Je vous remercie du fond du cœur.' }
    ]
  },
  {
    id: 3,
    term: 'Au revoir',
    definition: 'Goodbye',
    root: 'French "au" (until) + "revoir" (to see again)',
    examples: [
      { id: 5, sentence: 'Au revoir, à bientôt!' },
      { id: 6, sentence: 'Je lui ai dit au revoir avant de partir.' }
    ]
  }
]

const word = computed(() => words.find(w => w.id === parseInt(route.params.id)))
</script>