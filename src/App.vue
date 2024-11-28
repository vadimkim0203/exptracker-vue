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

import { ref, computed } from 'vue';

const toast = useToast();

const transactions = ref([
  { id: 1, text: "lunch", amount: -10.00 },
  { id: 2, text: "daiso", amount: -12.9 },
  { id: 3, text: "lotto", amount: -3.55 },
  { id: 4, text: "coupang", amount: -18.9 },
  { id: 5, text: "Salary", amount: 2500 },
]);

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
};

toast.success('Transaction added');

//id generation
const generateId = () => {
  return Math.floor(Math.random() * 10000000);
}

//delete transaction
const handleTransactionDeleted = (id) => {
  console.log(id);
}


</script>