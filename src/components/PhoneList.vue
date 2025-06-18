<template>
    <div class="phone-store">
      <h1 class="store-title">Toko HP Farhan</h1>
      
      <!-- Samsung Section -->
      <div class="brand-section">
        <h2 class="brand-title">Samsung</h2>
        <div class="phone-list">
          <div v-for="phone in samsungPhones" :key="phone.name" class="phone-item">
            <img :src="phone.imageUrl" :alt="phone.name" class="phone-image" />
            <h3 class="phone-name">{{ phone.name }}</h3>
            <p>Harga: Rp {{ formatPrice(phone.price) }}</p>
            <button class="btn-samsung" @click="showDetail(phone)">Lihat Detail</button>
            <button class="btn-buy" @click="showConfirmation(phone)">Beli Sekarang</button>
          </div>
        </div>
      </div>

      <!-- Apple Section -->
      <div class="brand-section">
        <h2 class="brand-title">Apple</h2>
        <div class="phone-list">
          <div v-for="phone in applePhones" :key="phone.name" class="phone-item">
            <img :src="phone.imageUrl" :alt="phone.name" class="phone-image" />
            <h3 class="phone-name">{{ phone.name }}</h3>
            <p>Harga: Rp {{ formatPrice(phone.price) }}</p>
            <button class="btn-apple" @click="showDetail(phone)">Lihat Detail</button>
            <button class="btn-buy" @click="showConfirmation(phone)">Beli Sekarang</button>
          </div>
        </div>
      </div>
      
      <!-- Menggunakan Modal Component -->
      <PhoneModal 
        v-if="showDetailModal || showModal" 
        :phone="selectedPhone"
        :modalType="modalType"
        @close="closeModal"
        @buy="handleBuy"
        @confirm="handleConfirm"
      />
    </div>
  </template>
  
  <script setup>
  import { ref } from 'vue'
  import PhoneModal from './PhoneModal.vue'
  
  const samsungPhones = [
    { 
      name: 'Samsung Galaxy S24 Ultra', 
      price: 19999000,
      imageUrl: 'https://i.pinimg.com/736x/24/22/32/24223258deb2711a6cfb6ffe2ba3b5e9.jpg',
      specs: [
        'Snapdragon 8 Gen 3',
        '12GB RAM + 256GB Storage',
        '6.8" Dynamic AMOLED 2X',
        '200MP Quad Camera',
        '5000mAh Battery'
      ]
    },
    { 
      name: 'Samsung Galaxy S24+', 
      price: 15999000,
      imageUrl: 'https://i.pinimg.com/736x/73/fe/05/73fe057cc91d5d608cd68b2c6c62b933.jpg',
      specs: [
        'Snapdragon 8 Gen 3',
        '12GB RAM + 256GB Storage',
        '6.7" Dynamic AMOLED 2X',
        '50MP Triple Camera',
        '4900mAh Battery'
      ]
    },
    { 
      name: 'Samsung Galaxy Z Flip6', 
      price: 17999000,
      imageUrl: 'https://i.pinimg.com/736x/cb/08/c0/cb08c093cc877cf8a123cf293698a6b2.jpg',
      specs: [
        'Snapdragon 8 Gen 3',
        '12GB RAM + 256GB Storage',
        '6.7" Foldable Dynamic AMOLED',
        '50MP Dual Camera',
        '4000mAh Battery'
      ]
    }
  ]

  const applePhones = [
    { 
      name: 'iPhone 15 Pro Max', 
      price: 21999000,
      imageUrl: 'https://i.pinimg.com/736x/29/3f/08/293f0849deb5e99702886be944549d10.jpg',
      specs: [
        'A17 Pro Chip',
        '8GB RAM + 256GB Storage',
        '6.7" Super Retina XDR',
        '48MP Pro Camera System',
        'USB-C with Thunderbolt'
      ]
    },
    { 
      name: 'iPhone 15 Pro', 
      price: 18999000,
      imageUrl: 'https://i.pinimg.com/736x/72/f0/8d/72f08df9bf96ab68e7e63da799ed13cd.jpg',
      specs: [
        'A17 Pro Chip',
        '8GB RAM + 128GB Storage',
        '6.1" Super Retina XDR',
        '48MP Pro Camera System',
        'USB-C with Thunderbolt'
      ]
    },
    { 
      name: 'iPhone 15', 
      price: 14999000,
      imageUrl: 'https://i.pinimg.com/736x/8e/1c/37/8e1c3744a4f11b8a6d5d053c59e9a75c.jpg',
      specs: [
        'A16 Bionic Chip',
        '6GB RAM + 128GB Storage',
        '6.1" Super Retina XDR',
        '48MP Main Camera',
        'USB-C Connector'
      ]
    }
  ]
  
  const showModal = ref(false)
  const showDetailModal = ref(false)
  const selectedPhone = ref(null)
  const modalType = ref('') // 'detail', 'confirm', 'success'
  
  const formatPrice = (price) => {
    return price.toLocaleString('id-ID')
  }
  
  const showConfirmation = (phone) => {
    selectedPhone.value = phone
    modalType.value = 'confirm'
    showModal.value = true
  }

  const showDetail = (phone) => {
    selectedPhone.value = phone
    modalType.value = 'detail'
    showDetailModal.value = true
  }

  const handleBuy = () => {
    showDetailModal.value = false
    modalType.value = 'confirm'
    showModal.value = true
  }

  const handleConfirm = () => {
    modalType.value = 'success'
  }

  const closeModal = () => {
    showModal.value = false
    showDetailModal.value = false
    selectedPhone.value = null
    modalType.value = ''
  }
  </script>
  
  <style scoped>
  .phone-store {
    background: linear-gradient(135deg, #1e3c72 0%, #2a5298 100%);
    min-height: 100vh;
    padding: 20px;
    font-family: 'Arial', sans-serif;
  }

  .store-title {
    text-align: center;
    color: white;
    font-size: 2.5rem;
    margin-bottom: 40px;
    text-shadow: 2px 2px 4px rgba(0,0,0,0.5);
  }

  .brand-section {
    margin-bottom: 50px;
  }

  .brand-title {
    color: white;
    font-size: 2rem;
    margin-bottom: 30px;
    text-align: center;
    text-shadow: 1px 1px 2px rgba(0,0,0,0.5);
  }
  
  .phone-list {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
    gap: 30px;
    max-width: 1200px;
    margin: 0 auto;
  }
  
  .phone-item {
    background: rgba(255, 255, 255, 0.1);
    backdrop-filter: blur(10px);
    border: 1px solid rgba(255, 255, 255, 0.2);
    border-radius: 20px;
    padding: 25px;
    text-align: center;
    transition: transform 0.3s ease, box-shadow 0.3s ease;
  }

  .phone-item:hover {
    transform: translateY(-10px);
    box-shadow: 0 20px 40px rgba(0,0,0,0.3);
  }
  
  .phone-image {
    width: 120px;
    height: 120px;
    object-fit: cover;
    border-radius: 15px;
    margin-bottom: 15px;
    border: 2px solid rgba(255,255,255,0.3);
  }
  
  .phone-name {
    color: white;
    font-size: 1.3rem;
    margin-bottom: 10px;
    font-weight: bold;
  }
  
  .phone-item p {
    color: #E0E0E0;
    font-size: 1.1rem;
    margin-bottom: 20px;
    font-weight: 600;
  }
  
  .btn-samsung {
    background: linear-gradient(45deg, #1f4788, #2962ff);
    color: white;
    border: none;
    padding: 12px 25px;
    border-radius: 25px;
    cursor: pointer;
    margin: 5px;
    font-weight: bold;
    transition: all 0.3s ease;
  }

  .btn-samsung:hover {
    background: linear-gradient(45deg, #1565c0, #2196f3);
    transform: scale(1.05);
  }

  .btn-apple {
    background: linear-gradient(45deg, #424242, #616161);
    color: white;
    border: none;
    padding: 12px 25px;
    border-radius: 25px;
    cursor: pointer;
    margin: 5px;
    font-weight: bold;
    transition: all 0.3s ease;
  }

  .btn-apple:hover {
    background: linear-gradient(45deg, #303030, #424242);
    transform: scale(1.05);
  }
  
  .btn-buy {
    background: linear-gradient(45deg, #4caf50, #66bb6a);
    color: white;
    border: none;
    padding: 12px 25px;
    border-radius: 25px;
    cursor: pointer;
    margin: 5px;
    font-weight: bold;
    transition: all 0.3s ease;
  }

  .btn-buy:hover {
    background: linear-gradient(45deg, #388e3c, #4caf50);
    transform: scale(1.05);
  }

  @media (max-width: 768px) {
    .phone-list {
      grid-template-columns: 1fr;
      gap: 20px;
    }
    
    .store-title {
      font-size: 2rem;
    }
    
    .brand-title {
      font-size: 1.5rem;
    }
  }
  </style>