<template>
  <div class="container mx-auto text-2xl py-8 max-w-xl">
    <h1 class="py-8 text-center text-white">
      List of all Capitals in the world
    </h1>
    <div class="grid grid-cols-2  mx-auto mb-4 border">
      <div
        class="p-3 text-right bg-indigo-100 text-md text-indigo-900 border border-solid border-4 border-gray-100"
      >
        Countries
      </div>
      <div class="p-3 text-white border border-solid border-4 border-gray-100">
        Capitals
      </div>
    </div>
    <div
      v-for="capital in Capitals"
      :key="capital.country"
      class="grid grid-cols-2 mx-auto bg-indigo-100 mb-4 border border-solid border-4 border-gray-100"
    >
      <div class="p-3 text-right text-sm">{{ capital.country }}</div>
      <div class="p-3 text-sm bg-indigo-900 text-white">{{ capital.city }}</div>
    </div>
  </div>
</template>

<script>
import { Capitals } from '@/assets/capitals'
export default {
  data: function() {
    return {
      Capitals
    }
  }
}
</script>

<style></style>
