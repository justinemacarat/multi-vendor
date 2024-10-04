<script setup>
    import { useRouter } from 'vue-router'
    import { onMounted } from 'vue'
    
    const router = useRouter()
    
    onMounted(() => {
        // Redirect to /vendor when the page is opened
        router.replace('/vendor')
    })

    useHead({
        title: 'Food Order Website',
    })
</script>
  