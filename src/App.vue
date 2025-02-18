<template>
    <div class="container mx-auto p-4">
      <h1 class="text-2xl  font-bold text-center mb-4 text-blue-400">Expense Tracker</h1>
      <AddTransaction @add-transaction="addTransaction" />
      <TransactionList 
        :transactions="transactions" 
        @delete-transaction="deleteTransaction"
      />
    </div>
  </template>
  
  <script>
  import { ref, onMounted } from 'vue';
  import AddTransaction from './components/AddTransaction.vue';
  import TransactionList from './components/TransactionList.vue';
  
  export default {
    components: { AddTransaction, TransactionList },
    setup() {
      const transactions = ref([]);
  
      onMounted(() => {
        const storedTransactions = localStorage.getItem('transactions');
        if (storedTransactions) {
          transactions.value = JSON.parse(storedTransactions);
        }
      });
  
      const saveTransactions = () => {
        localStorage.setItem('transactions', JSON.stringify(transactions.value));
      };
  
      const addTransaction = (transaction) => {
        if (transaction.amount <= 0) {
          alert("Amount must be greater than 0");
          return;
        }
        transactions.value.push(transaction);
        saveTransactions();
      };
  
      const deleteTransaction = (index) => {
        transactions.value.splice(index, 1);
        saveTransactions();
      };
  
      return { transactions, addTransaction, deleteTransaction };
    }
  };
  </script>