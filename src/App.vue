<template>
  <Header />
  <div class="container">
    <Balance :total="+total" />
    <IncomeExpenses :income="+income" :expenses="+expenses" />
    <Transactions :transactions="transactions" @transactionDeleted="handleTransactionDeleted" />
    <AddTransaction @transactionSubmitted="handleTransactionSubmitted" />
  </div>
</template>

<script setup>
import Header from "./components/Header.vue";
import Balance from "./components/Balance.vue";
import IncomeExpenses from "./components/IncomeExpenses.vue";
import Transactions from "./components/Transactions.vue";
import AddTransaction from "./components/AddTransaction.vue";

import { useToast } from "vue-toastification";

import { ref, computed, onMounted } from 'vue';

const toast = useToast();

const transactions = ref([]);
onMounted(() => {
  const savedTransactions = JSON.parse(localStorage.getItem('transactions'));
  if (savedTransactions) {
    transactions.value = savedTransactions
  };
});

//calcilating the total of income and spent
const total = computed((transaction) => {
  return transactions.value.reduce((acc, transaction) => {
    return acc + transaction.amount;
  }, 0)
});

//get income
const income = computed(() => {
  return transactions.value
    .filter((transaction) => transaction.amount > 0)
    .reduce((acc, transaction) => {
      return acc + transaction.amount;
    }, 0).toFixed(2);
});

//get expenses

const expenses = computed(() => {
  return transactions.value
    .filter((transaction) => transaction.amount < 0)
    .reduce((acc, transaction) => {
      return acc + transaction.amount;
    }, 0).toFixed(2);
});

//Add transaction

const handleTransactionSubmitted = (transactionData) => {
  transactions.value.push({
    id: generateId(),
    text: transactionData.text,
    amount: transactionData.amount,
  });

  saveTransactionsToLocalStorage();

  toast.success('Transaction added');

};


//id generation
const generateId = () => {
  return Math.floor(Math.random() * 10000000);
}

//delete transaction
const handleTransactionDeleted = (id) => {
  transactions.value = transactions.value.filter((transaction) => transaction.id !== id);

  saveTransactionsToLocalStorage();

  toast.success('Transaction deleted')
};

// Save to local storage

const saveTransactionsToLocalStorage = () => {
  localStorage.setItem("transactions", JSON.stringify(transactions.value))
};


</script>