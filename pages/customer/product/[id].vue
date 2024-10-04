<template>
    <div class="max-w-7xl mx-auto p-4">
      <div v-if="product" class="bg-white p-6 flex flex-col md:flex-row items-center">
        <img
          src="/assets/images/burger.jpg"
          alt="Product Image"
          class="w-full h-64 object-cover rounded-md mb-4 md:mb-0 md:w-1/3 md:mr-4"
        />
        <div class="flex-1">
          <h2 class="text-xl font-semibold">{{ product.name }}</h2>
          <p class="text-lg text-orange-500 mt-2">Price: ${{ product.price.toFixed(2) }} USD</p>
          <p class="text-gray-600 mt-4">{{ product.description }}</p>
          
          <label class="block mt-4">
            <span class="text-gray-700">Quantity:</span>
            <input
              type="number"
              v-model.number="quantity" 
              min="1"
              class="mt-1 p-2 block border-gray-300 rounded-md shadow-sm focus:border-blue-500 focus:ring focus:ring-blue-200"
            />
          </label>
          
          <div class="mt-6">
            <button
              @click.prevent="orderProduct(product.name, quantity)"
              class="bg-orange-500 text-white font-semibold py-2 px-4 rounded transition hover:bg-orange-600"
            >
              ORDER NOW
            </button>
          </div>
        </div>
      </div>
      <div v-else>
        <p>Product not found.</p>
      </div>
      <NuxtLink to="/customer" class="mt-4 inline-block text-blue-500 hover:underline">Back to Products</NuxtLink>
    </div>
  </template>
  
  <script setup>
  import { ref, onMounted } from 'vue'
  import { useRoute } from 'vue-router'
  
  const route = useRoute()
  const product = ref(null)
  const quantity = ref(1) // Reactive variable for quantity
  
  onMounted(() => {
    const productId = parseInt(route.params.id) // Retrieve the product ID from the URL
    const existingProducts = JSON.parse(localStorage.getItem('products')) || []
  
    product.value = existingProducts.find(prod => prod.id === productId) || null
  })
  
  const orderProduct = (productName, quantity) => {
    alert(`${quantity} of ${productName} has been ordered!`)
  }
  </script>
  