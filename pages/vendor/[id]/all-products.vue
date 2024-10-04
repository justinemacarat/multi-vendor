<template>
  <div>
    <h1 class="text-2xl font-bold mb-4">Products for {{ vendorName }}</h1>
    <div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-6">
      <div
        v-for="product in products"
        :key="product.id"
        class="bg-white border border-gray-300 rounded-lg shadow-md p-4 transition hover:shadow-lg"
      >
        <NuxtLink
          :to="`/customer/product/${product.id}`"
          class="text-lg font-semibold"
        >
          <img
              src="/assets/images/burger.jpg"
              alt="Product Image"
              class="w-full h-32 object-cover rounded-md mb-4"
          />
          <p class="text-center text-slate-950">{{ product.name }}</p>
          <p class="text-center text-gray-600 mt-2 text-sm">{{ product.description }}</p>
          <p class="text-center text-orange-500 mt-2">${{ product.price.toFixed(2) }}</p>
        </NuxtLink>
        <div class="text-center mt-4">
          <button
            @click.prevent="orderProduct(product.name)"
            class="bg-orange-500 text-white font-semibold py-2 px-4 rounded transition hover:bg-orange-600"
          >
            ORDER NOW
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import { useRouter } from 'vue-router'

// Get the router to access route parameters
const router = useRouter()
const route = router.currentRoute.value

const vendorId = route.params.id
const products = ref([])
const vendorName = ref('')

const fetchVendorProducts = () => {
  // Fetch all products from localStorage
  const allProducts = JSON.parse(localStorage.getItem('products')) || [];
  
  // Filter products for the specific vendor
  const storedProducts = allProducts.filter(product => product.vendorId == vendorId);

  // Set the products to the reactive variable
  products.value = storedProducts;

  // Set vendor name based on vendor ID (if you have names stored)
  const vendors = JSON.parse(localStorage.getItem('vendors')) || [];
  const vendor = vendors.find(v => v.id == vendorId);
  vendorName.value = vendor ? vendor.name : 'Unknown Vendor';
}

const orderProduct = (productName) => {
      alert(`${productName} has been ordered!`)
  }

onMounted(() => {
  fetchVendorProducts()
})
</script>
