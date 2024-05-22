<template>
    <div class="shoe-list">
      <div v-for="shoe in shoes" :key="shoe.name" class="shoe-item">
        <img :src="shoe.imageUrl" :alt="shoe.name" class="shoe-image" />
        <h3 class="shoe-name">{{ shoe.name }}</h3>
        <p>Harga: Rp {{ formatPrice(shoe.price) }}</p>
        <button class="btn-sage" @click="showConfirmation(shoe)">Pilih</button>
      </div>
      <!-- Modal for confirmation -->
      <div v-if="showModal" class="modal">
        <div class="modal-content">
          <p v-if="!thankYouMessage">Apakah Anda yakin ingin membeli {{ selectedShoe.name }}?</p>
          <p v-if="thankYouMessage">{{ thankYouMessage }}</p>
          <button v-if="!thankYouMessage" @click="confirmPurchase">Ya</button>
          <button v-if="!thankYouMessage" @click="cancelPurchase">Tidak</button>
          <button v-if="thankYouMessage" @click="closeModal">Tutup</button>
        </div>
      </div>
    </div>
  </template>
  
  <script setup>
  import { ref } from 'vue'
  
  const shoes = [
    { name: 'Asus ROG', price: 'Rp. 15.750.000', selectedSize: '', imageUrl: 'https://i.pinimg.com/564x/5e/18/8e/5e188e03791a1eca5ce4e6b98666ad38.jpg' },
    { name: 'Lenovo Legion', price: '12.400.000',  selectedSize: '', imageUrl: 'https://i.pinimg.com/564x/eb/35/4e/eb354e8c2b1c8ba61fb8700708310464.jpg' },
    { name: 'Hp Omen', price: ' 20.999.000' , selectedSize: '', imageUrl: 'https://i.pinimg.com/564x/f2/eb/5b/f2eb5ba30d3444034f4b2e801559787c.jpg' },
    { name: 'MSI Gaming', price: ' 10.900.000' , selectedSize: '', imageUrl: 'https://i.pinimg.com/736x/2b/97/99/2b9799e6efbc3f6345d26997268c605c.jpg' },
  ]
  
  const showModal = ref(false)
  const selectedShoe = ref(null)
  const thankYouMessage = ref('')
  
  const formatPrice = (price) => {
    return price.toLocaleString('id-ID')
  }
  
  const showConfirmation = (shoe) => {
    selectedShoe.value = shoe
    showModal.value = true
  }
  
  const confirmPurchase = () => {
    thankYouMessage.value = `Terima kasih telah membeli ${selectedShoe.value.name}!`
  }
  
  const cancelPurchase = () => {
    showModal.value = false
    selectedShoe.value = null
  }
  
  const closeModal = () => {
    showModal.value = false
    thankYouMessage.value = ''
  }
  </script>
  
  <style scoped>
  .shoe-list {
    display: flex;
    flex-wrap: wrap;
  }
  
  .shoe-item {
    margin: 20px;
    padding: 20px;
    border: 2px solid #333; /* Border lebih gelap */
    border-radius: 10px;
    text-align: center;
    background-color: #000000db; /* Background putih */
  }
  
  .shoe-image {
    width: 100px;
    height: 100px;
    object-fit: cover;
    margin-bottom: 10px;
  }
  
  .shoe-name, 
  .shoe-item p { /* Menambahkan selector untuk paragraf dalam .shoe-item */
    color: white; /* Warna teks putih */
  }
  
  .button {
    margin: 5px;
    padding: 15px 30px;
    border: none;
    border-radius: 10px;
    cursor: pointer;
  }
  
  .btn-sage {
    background-color: #9caf88;
    color: white;
    font-size: 16px;
    font-weight: bold;
    width: 200px;
    transition: background-color 0.3s ease;
  }
  
  .btn-sage:hover {
    background-color: #8ca379;
  }
  
  /* Modal styles */
  .modal {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.5);
    display: flex;
    align-items: center;
    justify-content: center;
  }
  
  .modal-content {
    background-color: #333; /* Background lebih gelap */
    padding: 20px;
    border-radius: 10px;
    text-align: center;
    color: white; /* Warna teks putih */
    border: 2px solid #fff; /* Border putih */
  }
  
  .modal-content p, 
  .modal-content button { /* Menambahkan selector untuk paragraf dalam .modal-content */
    color: white; /* Warna teks putih */
  }
  
  .modal-content button {
    margin: 10px;
    padding: 10px 20px;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    background-color: #9caf88; /* Background tombol */
    color: white;
  }
  
  .modal-content button:hover {
    background-color: #8ca379; /* Background tombol saat hover */
  }
  </style>
  