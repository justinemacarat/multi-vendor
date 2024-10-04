<template>
    <div class="max-w-7xl mx-auto p-4">
      <h1 class="text-2xl font-bold mb-4">Vendor Dashboard</h1>
      <table class="min-w-full bg-white border border-gray-300 rounded-lg shadow-md">
        <thead>
          <tr class="bg-gray-100 border-b">
            <th class="py-2 px-4 text-left text-gray-700">Product Name</th>
            <th class="py-2 px-4 text-left text-gray-700">Price (USD)</th>
            <th class="py-2 px-4 text-left text-gray-700 w-1/4">Description</th>
            <th class="py-2 px-4 text-left text-gray-700 text-center">Actions</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(product, index) in products" :key="index" class="border-b hover:bg-gray-50">
            <td class="py-2 px-4">{{ product.name }}</td>
            <td class="py-2 px-4">{{ product.price }}</td>
            <td class="py-2 px-4">{{ product.description }}</td>
            <td class="py-2 px-4 text-center">
              <button
                class="edit-button bg-green-500 text-white hover:bg-green-600 transition"
                @click="editProduct(index)"
              >
                Edit
              </button>
              <button
                class="delete-button bg-red-500 text-white hover:bg-red-600 transition"
                @click="deleteProduct(index)"
              >
                Delete
              </button>
            </td>
          </tr>
        </tbody>
      </table>
      <NuxtLink
        to="/vendor/add-product"
        class="mt-4 inline-block px-4 py-2 bg-blue-500 text-white rounded-lg hover:bg-blue-600 transition"
      >
        Add New Product
      </NuxtLink>
    </div>
  </template>
  
  <script setup>
    import { ref, onMounted } from 'vue'
    import { useRouter } from 'vue-router'
    
    const products = ref([])
    const router = useRouter()
    
    // Load products from local storage when the component mounts
    onMounted(() => {
        const existingProducts = JSON.parse(localStorage.getItem('products')) || []
        products.value = existingProducts
    })
  
    // Function to handle editing a product
    const editProduct = (index) => {
        router.push({ path: '/vendor/add-product', query: { id: index } })
    }
    
    // Function to handle deleting a product
    const deleteProduct = (index) => {
        products.value.splice(index, 1)
        localStorage.setItem('products', JSON.stringify(products.value))
    }
  
  </script>
  
  <style scoped>
    .edit-button,
    .delete-button {
        padding: 8px 12px;
        margin-right: 5px;
        border: none;
        border-radius: 4px;
        cursor: pointer;
    }
  </style>
  