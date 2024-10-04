<template>
    <div>
      <h1 class="text-3xl font-bold mb-4">Marketplace</h1>
      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4">
        <div 
          v-for="vendor in vendors" 
          :key="vendor.id" 
          class="bg-white p-4 rounded shadow transition hover:shadow-lg cursor-pointer"
          @click="goToVendorDashboard(vendor.id)"
        >
        <img src="/assets/images/burger.jpg" alt="Vendor Image" class="w-full h-32 object-cover rounded mb-2" />
          <h2 class="font-bold">{{ vendor.name }}</h2>
          <p class="text-gray-600"> {{ vendor.description }}</p>
        </div>
      </div>
    </div>
  </template>
  
  <script setup>
  import { onMounted, ref } from 'vue'
  import { useRouter } from 'vue-router'
  
  // Sample vendor data (you might want to replace this with a real API call)
  const vendors = ref([
    { id: 1, name: 'Vendor One', username: 'vendor1', description: 'Beverages' },
    { id: 2, name: 'Vendor Two', username: 'vendor2', description: 'Food' },
    { id: 3, name: 'Vendor Three', username: 'vendor3', description: 'Ice Cream' }
  ])
  
  const router = useRouter()
  
  // Method to redirect to vendor dashboard
  const goToVendorDashboard = (vendorId) => {
    router.push(`/vendor/${vendorId}/all-products`)
  }
  </script>
  