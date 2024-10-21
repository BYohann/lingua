<template>
  <table class="min-w-full bg-white border border-gray-300">
    <thead>
      <tr>
        <th v-for="column in columns" :key="column.accessorKey" class="px-4 py-2 bg-gray-100 border-b text-left">
          {{ column.header }}
        </th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="row in data" :key="row.id" class="border-b">
        <td v-for="column in columns" :key="column.accessorKey" class="px-4 py-2">
          <template v-if="column.accessorKey === 'examples'">
            <div v-for="example in row.examples" :key="example.id" class="mb-1">
              {{ example.sentence }}
            </div>
          </template>
          <template v-else>
            {{ row[column.accessorKey] }}
          </template>
        </td>
      </tr>
    </tbody>
  </table>
</template>

<script setup>
defineProps({
  data: {
    type: Array,
    required: true
  },
  columns: {
    type: Array,
    required: true
  }
})
</script>