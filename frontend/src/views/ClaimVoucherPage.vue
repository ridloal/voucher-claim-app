<template>
    <div class="max-w-2xl mx-auto bg-white rounded-lg shadow p-6">
      <h1 class="text-2xl font-bold text-gray-900 mb-6">
        Claim Your Voucher
      </h1>
      
      <form @submit.prevent="handleSubmit" class="space-y-4">
        <div>
          <label class="block text-gray-700 mb-2">Social Media Platform</label>
          <select 
            v-model="form.platform" 
            class="w-full p-2 border rounded-lg focus:ring-2 focus:ring-blue-500"
          >
            <option value="instagram">Instagram</option>
            <option value="tiktok">TikTok</option>
          </select>
        </div>
  
        <div>
          <label class="block text-gray-700 mb-2">Username</label>
          <input 
            type="text" 
            v-model="form.username"
            class="w-full p-2 border rounded-lg focus:ring-2 focus:ring-blue-500"
            placeholder="Your username"
          >
        </div>
  
        <div>
          <label class="block text-gray-700 mb-2">WhatsApp Number</label>
          <input 
            type="tel" 
            v-model="form.whatsapp"
            class="w-full p-2 border rounded-lg focus:ring-2 focus:ring-blue-500"
            placeholder="e.g., 08123456789"
          >
        </div>
  
        <div>
          <label class="block text-gray-700 mb-2">Email</label>
          <input 
            type="email" 
            v-model="form.email"
            class="w-full p-2 border rounded-lg focus:ring-2 focus:ring-blue-500"
            placeholder="your@email.com"
          >
        </div>
  
        <div class="space-y-2">
          <div class="flex items-center">
            <input 
              type="checkbox" 
              v-model="form.hasLiked"
              class="mr-2"
            >
            <span>I have liked the post</span>
          </div>
          <div class="flex items-center">
            <input 
              type="checkbox" 
              v-model="form.hasCommented"
              class="mr-2"
            >
            <span>I have commented on the post</span>
          </div>
          <div class="flex items-center">
            <input 
              type="checkbox" 
              v-model="form.hasShared"
              class="mr-2"
            >
            <span>I have shared the post</span>
          </div>
        </div>
  
        <button 
          type="submit"
          class="w-full bg-blue-600 text-white py-2 px-4 rounded-lg hover:bg-blue-700"
        >
          Verify & Claim
        </button>
      </form>
    </div>
  </template>
  
  <script>
  export default {
    name: 'ClaimVoucherPage',
    data() {
      return {
        form: {
          platform: 'instagram',
          username: '',
          whatsapp: '',
          email: '',
          hasLiked: false,
          hasCommented: false,
          hasShared: false
        }
      }
    },
    methods: {
      handleSubmit() {
        console.log('Form submitted:', this.form)
        // TODO: Implement API call
      }
    }
  }
  </script>