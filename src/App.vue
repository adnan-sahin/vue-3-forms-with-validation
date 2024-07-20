<script setup>
import Header from "@/components/Header.vue"
import Footer from "@/components/Footer.vue"
import PaymentView from "@/Views/PaymentView.vue"
import Error from "@/components/Error.vue"
// import { ref } from "vue"
import state from "@/state"

// const error = ref("")

// function setError(msg) {
//   error.value = msg
// }
</script>
<template>
  <Header />
  <Error :msg="state.error" />
  <PaymentView @onError="setError"></PaymentView>
  <Footer />
</template>
