<template>
  <Header />
  <div class="container">
    <Balance />
    <IncomeExpenses />
    <Transactions />
    <AddTransaction />
  </div>
</template>

<script>
import Header from "./components/Header.vue";
import Balance from "./components/Balance.vue";
import IncomeExpenses from "./components/IncomeExpenses.vue";
import Transactions from "./components/Transactions.vue";
import AddTransaction from "./components/AddTransaction.vue";

export default {
  components: {
    Header,
    Balance,
    IncomeExpenses,
    Transactions,
    AddTransaction,
  },
}
</script>