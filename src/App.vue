<template>
  <div>
    <header class="flex items-center justify-center py-3 px-4 bg-[#2c3d4e] shadow-lg">
      <router-link to="/">
        <h1 class="text-white text-3xl font-bold font-sans"><span class="text-[#42b883]">Vue</span>Movies</h1>
      </router-link>
    </header>
    <main>
      <router-view></router-view>
    </main>
  </div>
</template>


<script setup>

</script>


<style>
 body{
  background-color: #35495E;
 }
</style>
