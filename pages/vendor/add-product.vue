<template>
    <div class="max-w-md mx-auto p-4">
      <h1 class="text-2xl font-bold mb-4">{{ isEditMode ? 'Edit Product' : 'Add New Product' }}</h1>
      <form @submit.prevent="isEditMode ? updateProduct() : addProduct()" class="space-y-4">
        <label class="block">
          <span class="text-gray-700">Product Name:</span>
          <input
            type="text"
            v-model="productName"
            required
            class="mt-1 p-2 block w-full border-gray-300 rounded-md shadow-sm focus:border-blue-500 focus:ring focus:ring-blue-200"
          />
        </label>
        <label class="block">
          <span class="text-gray-700">Product Price (USD):</span>
          <input
            type="number"
            v-model="productPrice"
            min="0"
            required
            class="mt-1 p-2 block w-full border-gray-300 rounded-md shadow-sm focus:border-blue-500 focus:ring focus:ring-blue-200"
          />
        </label>
        <label class="block">
          <span class="text-gray-700">Product Description:</span>
          <textarea
            v-model="productDescription"
            required
            rows="4"
            class="mt-1 p-2 block w-full border-gray-300 rounded-md shadow-sm focus:border-blue-500 focus:ring focus:ring-blue-200"
          ></textarea>
        </label>
        <button
          type="submit"
          class="w-full px-4 py-2 font-semibold text-white bg-blue-500 rounded-md hover:bg-blue-600 transition"
        >
          {{ isEditMode ? 'Update Product' : 'Add Product' }}
        </button>
      </form>
      <NuxtLink to="/vendor" class="mt-4 inline-block text-blue-500 hover:underline">Back to Dashboard</NuxtLink>
    </div>
  </template>
  
  <script setup>
  import { ref, onMounted } from 'vue'
  import { useRouter, useRoute } from 'vue-router'
  
  // Reactive variables
  const productName = ref('')
  const productPrice = ref(0)
  const productDescription = ref('')
  const isEditMode = ref(false)
  const editId = ref(null)

  const router = useRouter()
  const route = useRoute()
  
  // Function to handle adding a new product
  const addProduct = () => {
    const existingProducts = JSON.parse(localStorage.getItem('products')) || []
  
    // Create a new product object with an ID based on the current length of the array
    const newProduct = { 
      id: existingProducts.length, // Using the length of the array as the unique ID
      name: productName.value, 
      price: productPrice.value,
      description: productDescription.value,
    }
  
    // Add the new product to the existing products array
    existingProducts.push(newProduct)
    localStorage.setItem('products', JSON.stringify(existingProducts))
    resetFields()
    router.push('/vendor')
  }
  
  // Function to handle updating an existing product
  const updateProduct = () => {
    const existingProducts = JSON.parse(localStorage.getItem('products')) || []
    const productIndex = existingProducts.findIndex(product => product.id === editId.value)
  
    // Update the product object in the array
    if (productIndex !== -1) {
      existingProducts[productIndex] = {
        id: editId.value,
        name: productName.value,
        price: productPrice.value,
        description: productDescription.value,
      }
      localStorage.setItem('products', JSON.stringify(existingProducts))
    }
  
    resetFields()
    router.push('/vendor')
  }
  
  // Function to reset input fields
  const resetFields = () => {
    productName.value = ''
    productPrice.value = 0
    productDescription.value = ''
  }
  
  // Load product details if in edit mode
  onMounted(() => {
    if (route.query.id !== undefined) {
      isEditMode.value = true
      editId.value = parseInt(route.query.id) // Get the ID from the query params
      const existingProducts = JSON.parse(localStorage.getItem('products')) || []
  
      // Find the product by ID
      const product = existingProducts.find(product => product.id === editId.value)
      if (product) {
        productName.value = product.name
        productPrice.value = product.price
        productDescription.value = product.description
      }
    }
  })
  </script>
  