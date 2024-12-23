<template>
  <div id="app" class="min-h-screen bg-gray-100">
    <nav class="bg-gray-800 text-white p-4">
      <div class="container mx-auto">
        <router-link to="/" class="mr-4 hover:text-gray-300">Home</router-link>
        <router-link to="/claim" class="mr-4 hover:text-gray-300">Claim Voucher</router-link>
      </div>
    </nav>
    
    <main class="container mx-auto px-4 py-8">
      <router-view/>
    </main>
  </div>
</template>

<script>
export default {
  name: 'App'
}
</script>