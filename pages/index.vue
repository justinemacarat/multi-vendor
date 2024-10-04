<script setup>
  import { onMounted, ref } from 'vue'
  import { useRouter } from 'vue-router'
  
  // Sample vendor data (you might want to replace this with a real API call)
  const vendors = ref([
    { id: 1, name: 'Vendor One', username: 'vendor1', password: 'password1', description: 'Beverages' },
    { id: 2, name: 'Vendor Two', username: 'vendor2', password: 'password2', description: 'Food' },
    { id: 3, name: 'Vendor Three', username: 'vendor3', password: 'password3', description: 'Ice Cream' }
  ])
  
  const router = useRouter()
  
  onMounted(() => {
    localStorage.setItem('vendors', JSON.stringify(vendors.value))
    router.replace('/marketplace')
  })
  </script>
  