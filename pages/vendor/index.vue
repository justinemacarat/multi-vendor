<script setup>
import { onMounted } from 'vue'
import { useRouter } from 'vue-router'

// Get the router instance
const router = useRouter()

onMounted(() => {
  // Check if the vendor is logged in
  const isVendorLoggedIn = localStorage.getItem('isVendorLoggedIn')

  // If not logged in, redirect to the login page
  if (!isVendorLoggedIn) {
    router.replace('/vendor/login')
  }
})
</script>
