<script setup>
defineProps({
  msg: String,
})
</script>

<template>
  <div class="bg-red-700 text-white w-full my-2" v-if="msg">{{ msg }}</div>
</template>

<style lang="scss" scoped></style>
