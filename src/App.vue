<template>
  <div id="app">
    <nav class="text-center mt-4 mb-4">
      <h2>
        <router-link :to="{name:'home'}" v-show="this.$route.name === 'add' || this.$route.name === 'edit'">Home</router-link>
      </h2>

      <h2>
        <router-link :to="{name:'add'}" v-show="this.$route.name === 'home'">Add</router-link>
      </h2>
    </nav>
    <router-view/>
  </div>
</template>
<style>

</style>
<script setup>
</script>