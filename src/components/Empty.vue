<template>
  <div class="flex flex-col items-center mx-auto">
    <img src="../assets/images/empty.svg" class="mt-8 h-64 w-auto block mx-auto">
    <h1 class="text-2xl font-semibold">You have no stocks yet</h1>
    <p class="text-gray-700 mb-4">Why don't you try to purchase one?</p>
    <router-link to="/stocks" class="btn" tag="button">Get Stock</router-link>
  </div>
</template>