<template>
  <div class="customers" v-if="customer" v-bind:class="{'is-gold': customer.isGold}">
    <input type="checkbox" v-on:change="markGold">
    <div class="customer-name" v-if="customer" >{{ customer.name }}</div>
    <div class="customer-phone" v-if="customer">{{ customer.phone }}</div>
  </div>
</template>

<script>
  import axios from 'axios'

  export default {
    name: 'Customers',
    methods: {
      markGold() {
        const customer = {...this.customer, isGold: !this.customer.isGold}

        axios.post('http://localhost:7000/api/customers', customer)
          .then(res => console.log(res))
      }
    }
  }
</script>

<style scoped>
  .customers {
    background: #f4f4f4;
    width: 100%;
    display: flex;
    justify-content: space-between;
  }
  .is-complete {
    background: gold;
  }
</style>