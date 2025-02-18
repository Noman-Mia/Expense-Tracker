<template>
    <div>
      <table class="w-full border-collapse border border-gray-300">
        <thead>
          <tr>
            <th class="border border-gray-300 text-cyan-50 px-4 py-2">Title</th>
            <th class="border border-gray-300 text-cyan-50 px-4 py-2">Amount</th>
            <th class="border border-gray-300 text-cyan-50 px-4 py-2">Type</th>
            <th class="border border-gray-300 text-cyan-50 px-4 py-2">Actions</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(transaction, index) in transactions" :key="index">
            <td class="border border-gray-300 px-4 py-2 text-blue-50">{{ transaction.title }}</td>
            <td 
              class="border border-gray-300 px-4 py-2"
              :class="{ 'font-bold': transaction.amount >= 500, 'text-green-500': transaction.type === 'Income', 'text-red-500': transaction.type === 'Expense' }"
            >
              ${{ transaction.amount }}
            </td>
            <td class="border border-gray-300 px-4 py-2 uppercase text-blue-50">{{ transaction.type }}</td>
            <td class="border border-gray-300 px-4 py-2 text-blue-50">
              <button @click="deleteTransaction(index)" class="bg-red-500 text-white px-2 py-1 rounded">Delete</button>
            </td>
          </tr>
          <tr v-if="transactions.length === 0">
            <td colspan="4" class="text-center py-4 text-blue-50">No transactions recorded yet.</td>
          </tr>
        </tbody>
      </table>
    </div>
  </template>
  
  <script setup>
  import { defineProps, defineEmits } from 'vue';
  
  const props = defineProps({
    transactions: Array
  });
  
  const emit = defineEmits(['delete-transaction']);
  
  const deleteTransaction = (index) => {
    emit('delete-transaction', index);
  };
  </script>
  