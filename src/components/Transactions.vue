<template>
  <h3>History</h3>
  <li v-for="transaction in transactions" v-bind:key="transaction.id"
    v-bind:class="transaction.amount < 0 ? 'minus' : 'plus'">
    {{ transaction.text }} <span>-${{ transaction.amount }}</span><button class="delete-btn">x</button>
  </li>
  <!-- <ul id="list" class="list">
    <li class="minus">
      Cash <span>-$400</span><button class="delete-btn">x</button>
    </li>
    <li class="plus">
      Monthly salary <span>$2000</span><button class="delete-btn">x</button>
    </li> 
  </ul> -->
</template>

<script>
export default {
  data() {
    return {
      transactions: [
        { id: 1, text: "lunch", amount: -10.00 },
        { id: 2, text: "daiso", amount: -12.89 },
        { id: 3, text: "lotto", amount: -3.55 },
        { id: 4, text: "coupang", amount: -18.29 },

      ],
    }
  }
}
</script>