<template>
  <div>
    <h1 class="welcome-heading">Selamat Datang di Toko Laptop NaufalRizh</h1>
    <DaftarLaptop />
  </div>
</template>

<script>
import DaftarLaptop from './components/DaftarLaptop.vue';

export default {
  components: { DaftarLaptop }
}
</script>

<style scoped>
.welcome-heading {
  background-color: black;
  color: white;
  font-family: Cambria, 'Times New Roman', Times, serif;
  text-align: center;
  padding: 20px;
}
</style>
