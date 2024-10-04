<template>
  <div class="flex flex-col min-h-screen">
    <NuxtRouteAnnouncer />
    <header class="bg-gray-800 text-white p-4">
      <div class="container mx-auto flex justify-between items-center">
        <h1 class="text-xl font-bold">Food Order Website</h1>
        <nav>
          <ul class="flex space-x-4">
            <li>
              <NuxtLink to="/vendor" class="hover:text-gray-300">Vendor Dashboard</NuxtLink>
            </li>
            <li>
              <NuxtLink to="/customer" class="hover:text-gray-300">Customer Dashboard</NuxtLink>
            </li>
          </ul>
        </nav>
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

