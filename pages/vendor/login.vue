<template>
    <div class="flex items-center justify-center h-[calc(100vh-150px)] overflow-auto">
      <div class="bg-white p-8 rounded shadow-md w-full max-w-md">
        <h2 class="text-2xl font-bold mb-6">Vendor Login</h2>
        <form @submit.prevent="loginVendor" class="space-y-4">
          <label class="block">
            <span class="text-gray-700">Username:</span>
            <input
              type="text"
              v-model="username"
              required
              class="mt-1 p-2 block w-full border-gray-300 rounded-md shadow-sm focus:border-blue-500 focus:ring focus:ring-blue-200"
            />
          </label>
          <label class="block">
            <span class="text-gray-700">Password:</span>
            <input
              type="password"
              v-model="password"
              required
              class="mt-1 p-2 block w-full border-gray-300 rounded-md shadow-sm focus:border-blue-500 focus:ring focus:ring-blue-200"
            />
          </label>
          <button
            type="submit"
            class="w-full px-4 py-2 font-semibold text-white bg-blue-500 rounded-md hover:bg-blue-600 transition"
          >
            Login
          </button>
        </form>
        <p v-if="errorMessage" class="mt-4 text-red-500">{{ errorMessage }}</p>
      </div>
    </div>
  </template>
  
  <script setup>
  import { ref } from 'vue'
  import { useRouter } from 'vue-router'
  
  // Reactive form fields
  const username = ref('')
  const password = ref('')
  const errorMessage = ref('')
  
  const router = useRouter()
  
  // Array of vendors with their credentials and IDs
  const vendors = [
    { id: 1, username: 'vendor1', password: 'password1' },
    { id: 2, username: 'vendor2', password: 'password2' },
    { id: 3, username: 'vendor3', password: 'password3' }
  ]
  
  const loginVendor = () => {
    // Find the matching vendor based on the provided username and password
    const vendor = vendors.find(v => v.username === username.value && v.password === password.value)
  
    if (vendor) {
      // Save the vendor's login state and ID in localStorage
      localStorage.setItem('isVendorLoggedIn', 'true')
      localStorage.setItem('vendorId', vendor.id)
  
      // Redirect to the vendor dashboard
      router.push(`/vendor/${vendor.id}`)
    } else {
      errorMessage.value = 'Invalid username or password.'
    }
  }
  </script>
  