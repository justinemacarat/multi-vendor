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
  
  onMounted(() => {
    router.replace('/marketplace')
  })
  </script>
  