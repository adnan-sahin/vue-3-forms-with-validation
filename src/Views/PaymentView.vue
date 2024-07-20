<script setup>
import { watch } from 'vue'
import months from '@/lookup/months'
import AddressView from '@/Views/AddressView.vue'
import state from '@/state'

const years = Array.from({ length: 20 }, (_, i) => i + new Date().getFullYear())

function onSubmit() {
  state.error = "Can't save yet,no API"
}

watch(
  () => state.billing.sameAsShipping,
  () => {
    if (state.billing.sameAsShipping) {
      Object.keys(state.shipping).forEach((key) => {
        state.billing[key] = state.shipping[key]
      })
    }
  }
)
</script>

<template>
  <div class="container bg-blue-300 mx-auto p-2">
    <h2>Payment</h2>
    <div>
      <form novalidate @submit.prevent="onSubmit">
        <div class="grid grid-cols-2 gap-2">
          <div>
            <AddressView :model="state.shipping">
              <h3 class="mb-6">Shipping Address</h3>
            </AddressView>
          </div>
          <div>
            <AddressView :model="state.billing" :isDisabled="state.billing.sameAsShipping">
              <h3>Billing</h3>
              <label class="flex">
                <input type="checkbox" v-model="state.billing.sameAsShipping" />
                &nbsp; Same as Shipping?
              </label>
            </AddressView>
          </div>
        </div>
        <div class="w-1/2 border rounded p-1 mt-2 bg-gray-100">
          <div>
            <h3>Credit Card</h3>
            <label for="cardNumber"> Card Number</label>
            <input type="text" id="cardNumber" v-model="state.creditCard.number" />
            <label for="cardHolder"> Name on Card</label>
            <input type="text" id="cardHolder" v-model="state.creditCard.nameOnCard" />
            <div class="grid grid-cols-3 gap-2">
              <div>
                <label for="exMonth">Expiration Month</label>
                <select id="exMonth" v-model="state.creditCard.expirationMonth">
                  <option v-for="month in months" :value="month.number" :key="month.number">
                    {{ month.name }}
                  </option>
                </select>
              </div>
              <div>
                <label for="exYear">Expiration Year</label>
                <select id="exYear" v-model="state.creditCard.expirationYear">
                  <option v-for="year in years" :value="year" :key="year">
                    {{ year }}
                  </option>
                </select>
              </div>
              <div>
                <label for="cardCCV"> Card CCV</label>
                <input type="text" id="cardCCV" v-model="state.creditCard.cvv" />
              </div>
            </div>
          </div>
        </div>
        <button type="submit" @click="alert('Hi')">Next</button>
      </form>
      <div>
        <pre>{{ state }}</pre>
      </div>
    </div>
  </div>
</template>

<style lang="scss" scoped></style>
