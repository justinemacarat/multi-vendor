<template>
    <div>
      <h1 class="text-3xl font-bold mb-4">Marketplace</h1>
      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4">
        <div 
          v-for="vendor in vendors" 
          :key="vendor.id" 
          class="bg-white p-4 rounded shadow transition hover:shadow-lg cursor-pointer"
          @click="goToAllProducts(vendor.id)"
        >
          <img src="/assets/images/burger.jpg" alt="Vendor Image" class="w-full h-32 object-cover rounded mb-2" />
          <h2 class="font-bold">{{ vendor.name }}</h2>
          <p class="text-gray-600">{{ vendor.description }}</p>
        </div>
      </div>
    </div>
  </template>
  
  <script setup>
  import { onMounted, ref } from 'vue'
  import { useRouter } from 'vue-router'
  
  const vendors = ref([])
  
  const router = useRouter()
  
  onMounted(() => {
    // Check if running on the client side
    if (process.client) {
      const storedVendors = localStorage.getItem('vendors')
      vendors.value = storedVendors ? JSON.parse(storedVendors) : []
    }
  })
  
  const goToAllProducts = (vendorId) => {
    router.push(`/vendor/${vendorId}/all-products`)
  }
  </script>
  