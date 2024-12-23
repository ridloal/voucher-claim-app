<template>
  <div class="space-y-6">
    <section class="bg-white rounded-lg shadow p-6">
      <h1 class="text-3xl font-bold text-gray-900 mb-4">
        Welcome to Voucher Claim
      </h1>
      <p class="text-gray-600">
        Get amazing discounts by participating in our social media campaign!
      </p>
    </section>

    <section class="bg-white rounded-lg shadow p-6">
      <h2 class="text-2xl font-bold text-gray-900 mb-4">Best Sellers</h2>
      <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
        <!-- Example product card -->
        <div class="border rounded-lg p-4">
          <div class="aspect-w-1 aspect-h-1 bg-gray-200 rounded-lg mb-4">
            <!-- Product image placeholder -->
            <div class="w-full h-48 bg-gray-300 rounded-lg"></div>
          </div>
          <h3 class="text-lg font-semibold">Product Name</h3>
          <p class="text-gray-600">Rp 199.000</p>
          <div class="flex items-center mt-2">
            <span class="text-yellow-400">★★★★☆</span>
            <span class="text-gray-600 text-sm ml-2">(4.0)</span>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
export default {
  name: "HomePage",
};
</script>
