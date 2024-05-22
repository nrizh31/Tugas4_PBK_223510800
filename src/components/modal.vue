<template>
    <div class="modal-overlay" @click="closeModal">
      <div class="modal-content" @click.stop>
        <h3 style="color: white;">Detail Laptop</h3> <!-- Menambahkan warna putih pada teks -->
        <img :src="laptop.imageUrl" :alt="laptop.name" class="laptop-image" />
        <p style="color: white;">Nama: {{ laptop.name }}</p> <!-- Menambahkan warna putih pada teks -->
        <p style="color: white;">Harga: Rp {{ formatPrice(laptop.price) }}</p> <!-- Menambahkan warna putih pada teks -->
        <p style="color: white;">Spesifikasi:</p> <!-- Menambahkan warna putih pada teks -->
        <ul>
          <li v-for="(spec, index) in laptop.spec" :key="index" style="color: white;">{{ spec }}</li> <!-- Menambahkan warna putih pada teks -->
        </ul>
        <button @click="buyLaptop">Beli</button>
        <button @click="closeModal">Tutup</button>
      </div>
    </div>
  </template>
  
  <script setup>
  import { ref, watch, defineProps, defineEmits } from 'vue'
  
  const props = defineProps({
    laptop: Object
  })
  
  const emit = defineEmits(['close'])
  
  const totalPrice = ref(parseFloat(props.laptop.price.replace(/[^0-9.-]+/g,"")))
  
  watch(() => props.laptop.price, (newPrice) => {
    totalPrice.value = parseFloat(newPrice.replace(/[^0-9.-]+/g,""))
  })
  
  const formatPrice = (price) => {
    return price.toLocaleString('id-ID')
  }
  
  const closeModal = () => {
    emit('close')
  }
  
  const buyLaptop = () => {
    alert(`Anda telah membeli laptop ${props.laptop.name} dengan harga Rp ${formatPrice(totalPrice.value)}`)
    closeModal()
  }
  </script>
  
  <style scoped>
  .modal-overlay {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: rgba(0, 0, 0, 0.5);
    display: flex;
    align-items: center;
    justify-content: center;
  }
  
  .modal-content {
    background: white;
    color: black;
    padding: 20px;
    border-radius: 10px;
    text-align: center;
    position: relative;
    color: white; /* Menambahkan warna putih untuk teks */
  }
  </style>
  