<template>
  <div class="flex flex-col min-h-screen">
    <NuxtRouteAnnouncer />
    <header class="bg-gray-800 text-white p-4">
      <div class="container mx-auto flex justify-between items-center">
        <h1 class="text-xl font-bold">Food Order Website</h1>
      </div>
    </header>
    <main class="flex-grow container mx-auto p-4">
      <NuxtPage />
    </main>
    <footer class="bg-gray-800 text-white p-4">
      <div class="container mx-auto text-center">
        <p>© 2024 Food Order Website</p>
      </div>
    </footer>
  </div>
</template>

<script setup>

  useHead({
    title: 'Food Order Website',
  })

</script>