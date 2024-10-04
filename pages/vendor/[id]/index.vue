<template>
  <div class="max-w-7xl mx-auto p-4">
      <div class="flex justify-end mb-2">
        <button @click="logoutVendor" class="px-4 py-2 bg-red-500 text-white rounded">
          Logout
        </button>
      </div>
      <h1 class="text-2xl font-bold mb-4">Vendor Dashboard</h1>
      <!-- Products Table -->
      <div class="overflow-x-auto">
        <table class="min-w-full bg-white border border-gray-300 rounded-lg shadow-md">
          <thead>
            <tr class="bg-gray-100 border-b">
              <th class="py-2 px-4 text-left text-gray-700">Product Name</th>
              <th class="py-2 px-4 text-left text-gray-700">Price (USD)</th>
              <th class="py-2 px-4 text-left text-gray-700 w-1/4">Description</th>
              <th class="py-2 px-4 text-center text-gray-700">Actions</th>
            </tr>
          </thead>
          <tbody>
            <tr v-if="filteredProducts.length === 0">
              <td colspan="4" class="py-4 text-center text-gray-500">No products found.</td>
            </tr>
            <tr
              v-for="(product, index) in filteredProducts"
              :key="index"
              class="border-b hover:bg-gray-50"
            >
              <td class="py-2 px-4">{{ product.name }}</td>
              <td class="py-2 px-4">{{ product.price }}</td>
              <td class="py-2 px-4">{{ product.description }}</td>
              <td class="py-2 px-4 text-center">
                <button
                  class="edit-button bg-green-500 text-white hover:bg-green-600 transition mb-2 lg:mb-0"
                  @click="editProduct(product.id)"
                >
                  Edit
                </button>
                <button
                  class="delete-button bg-red-500 text-white hover:bg-red-600 transition"
                  @click="deleteProduct(product.id)"
                >
                  Delete
                </button>
              </td>
            </tr>
          </tbody>
        </table>
      </div>

      <!-- Add New Product Link -->
      <NuxtLink
        :to="`/vendor/${vendorId}/add-product`"
        class="mt-4 inline-block px-4 py-2 bg-blue-500 text-white rounded-lg hover:bg-blue-600 transition"
      >
        Add New Product
      </NuxtLink>
  </div>
</template>

<script setup>
  import { ref, computed, onMounted } from 'vue'
  import { useRouter, useRoute } from 'vue-router'

  const products = ref([])
  const router = useRouter()
  const route = useRoute()
  const vendorId = ref(null)

  onMounted(() => {
    const existingProducts = JSON.parse(localStorage.getItem('products')) || []
    products.value = existingProducts
    vendorId.value = route.params.id // Get vendor ID from the route
  })

  const filteredProducts = computed(() => {
    return products.value.filter(product => product.vendorId === vendorId.value)
  })

  const editProduct = (productId) => {
    router.push({ path: `/vendor/${vendorId.value}/add-product`, query: { id: productId } })
  }

  const deleteProduct = (productId) => {
    const productIndex = products.value.findIndex(product => product.id === productId)
    if (productIndex !== -1) {
      products.value.splice(productIndex, 1)
      localStorage.setItem('products', JSON.stringify(products.value))
    }
  }

  const logoutVendor = () => {
    localStorage.removeItem('isVendorLoggedIn')
    localStorage.removeItem('vendorId')
    router.push('/vendor/login')
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

/* Responsive table cells for small screens */

</style>
