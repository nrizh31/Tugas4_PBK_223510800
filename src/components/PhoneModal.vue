<template>
    <div class="modal" @click="closeModal">
      <div class="modal-content" @click.stop>
        
        <!-- Detail Modal -->
        <div v-if="modalType === 'detail'" class="detail-modal">
          <h3>Detail {{ phone.name }}</h3>
          <img :src="phone.imageUrl" :alt="phone.name" class="detail-image" />
          <p><strong>Nama:</strong> {{ phone.name }}</p>
          <p><strong>Harga:</strong> Rp {{ formatPrice(phone.price) }}</p>
          <p><strong>Spesifikasi:</strong></p>
          <ul class="spec-list">
            <li v-for="(spec, index) in phone.specs" :key="index">{{ spec }}</li>
          </ul>
          <div class="modal-buttons">
            <button class="btn-buy" @click="buyFromDetail">Beli Sekarang</button>
            <button class="btn-close" @click="closeModal">Tutup</button>
          </div>
        </div>

        <!-- Confirmation Modal -->
        <div v-if="modalType === 'confirm'" class="confirm-modal">
          <h3>Konfirmasi Pembelian</h3>
          <img :src="phone.imageUrl" :alt="phone.name" class="confirm-image" />
          <p>Apakah Anda yakin ingin membeli <strong>{{ phone.name }}</strong>?</p>
          <p>Harga: <strong>Rp {{ formatPrice(phone.price) }}</strong></p>
          <div class="modal-buttons">
            <button class="btn-confirm" @click="confirmPurchase">Ya, Beli</button>
            <button class="btn-cancel" @click="closeModal">Batal</button>
          </div>
        </div>

        <!-- Success Modal -->
        <div v-if="modalType === 'success'" class="success-modal">
          <div class="success-icon">✓</div>
          <h3>Pembelian Berhasil!</h3>
          <p>Terima kasih telah membeli <strong>{{ phone.name }}</strong>!</p>
          <p>Pesanan Anda akan segera diproses dan dikirim ke alamat tujuan.</p>
          <div class="order-info">
            <p><strong>Total Pembayaran:</strong> Rp {{ formatPrice(phone.price) }}</p>
            <p><strong>Estimasi Pengiriman:</strong> 1-3 hari kerja</p>
          </div>
          <button class="btn-close" @click="closeModal">Tutup</button>
        </div>

      </div>
    </div>
  </template>
  
  <script setup>
  import { defineProps, defineEmits } from 'vue'
  
  const props = defineProps({
    phone: {
      type: Object,
      required: true
    },
    modalType: {
      type: String,
      required: true // 'detail', 'confirm', 'success'
    }
  })
  
  const emit = defineEmits(['close', 'buy', 'confirm'])
  
  const formatPrice = (price) => {
    return price.toLocaleString('id-ID')
  }
  
  const closeModal = () => {
    emit('close')
  }
  
  const buyFromDetail = () => {
    emit('buy')
  }

  const confirmPurchase = () => {
    emit('confirm')
  }
  </script>
  
  <style scoped>
  .modal {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.7);
    display: flex;
    align-items: center;
    justify-content: center;
    z-index: 1000;
    animation: fadeIn 0.3s ease;
  }

  @keyframes fadeIn {
    from { opacity: 0; }
    to { opacity: 1; }
  }
  
  .modal-content {
    background: linear-gradient(135deg, #2d3748, #4a5568);
    padding: 30px;
    border-radius: 20px;
    text-align: center;
    color: white;
    border: 2px solid rgba(255, 255, 255, 0.3);
    max-width: 600px;
    max-height: 80vh;
    overflow-y: auto;
    box-shadow: 0 25px 50px rgba(0, 0, 0, 0.5);
    animation: slideIn 0.3s ease;
  }

  @keyframes slideIn {
    from { transform: translateY(-50px); opacity: 0; }
    to { transform: translateY(0); opacity: 1; }
  }

  /* Detail Modal Styles */
  .detail-modal h3 {
    color: white;
    margin-bottom: 20px;
    font-size: 1.8rem;
    text-shadow: 1px 1px 2px rgba(0,0,0,0.5);
  }

  .detail-image {
    width: 150px;
    height: 150px;
    object-fit: cover;
    border-radius: 15px;
    margin: 20px auto;
    display: block;
    border: 3px solid rgba(255,255,255,0.3);
    box-shadow: 0 10px 20px rgba(0,0,0,0.3);
  }

  .spec-list {
    text-align: left;
    background: rgba(255, 255, 255, 0.1);
    padding: 20px;
    border-radius: 15px;
    margin: 20px 0;
    backdrop-filter: blur(10px);
  }

  .spec-list li {
    margin: 10px 0;
    padding: 8px 0;
    border-bottom: 1px solid rgba(255,255,255,0.2);
    font-size: 1rem;
  }

  .spec-list li:last-child {
    border-bottom: none;
  }

  /* Confirmation Modal Styles */
  .confirm-modal h3 {
    color: white;
    margin-bottom: 20px;
    font-size: 1.6rem;
  }

  .confirm-image {
    width: 100px;
    height: 100px;
    object-fit: cover;
    border-radius: 10px;
    margin: 15px auto;
    display: block;
    border: 2px solid rgba(255,255,255,0.3);
  }

  /* Success Modal Styles */
  .success-modal {
    text-align: center;
  }

  .success-icon {
    width: 80px;
    height: 80px;
    background: #4caf50;
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    margin: 0 auto 20px;
    font-size: 40px;
    color: white;
    font-weight: bold;
    animation: pulse 2s infinite;
  }

  @keyframes pulse {
    0% { transform: scale(1); }
    50% { transform: scale(1.05); }
    100% { transform: scale(1); }
  }

  .success-modal h3 {
    color: #4caf50;
    margin-bottom: 15px;
    font-size: 1.8rem;
  }

  .order-info {
    background: rgba(76, 175, 80, 0.1);
    padding: 15px;
    border-radius: 10px;
    margin: 20px 0;
    border: 1px solid rgba(76, 175, 80, 0.3);
  }

  /* Button Styles */
  .modal-buttons {
    margin-top: 25px;
    display: flex;
    gap: 15px;
    justify-content: center;
    flex-wrap: wrap;
  }

  .btn-buy, .btn-confirm {
    background: linear-gradient(45deg, #4caf50, #66bb6a);
    color: white;
    border: none;
    padding: 15px 30px;
    border-radius: 25px;
    cursor: pointer;
    font-weight: bold;
    font-size: 1rem;
    transition: all 0.3s ease;
    min-width: 120px;
  }

  .btn-buy:hover, .btn-confirm:hover {
    background: linear-gradient(45deg, #388e3c, #4caf50);
    transform: scale(1.05);
  }

  .btn-cancel, .btn-close {
    background: linear-gradient(45deg, #f44336, #ef5350);
    color: white;
    border: none;
    padding: 15px 30px;
    border-radius: 25px;
    cursor: pointer;
    font-weight: bold;
    font-size: 1rem;
    transition: all 0.3s ease;
    min-width: 120px;
  }

  .btn-cancel:hover, .btn-close:hover {
    background: linear-gradient(45deg, #d32f2f, #f44336);
    transform: scale(1.05);
  }

  /* Text Styles */
  .modal-content p {
    color: white;
    margin: 15px 0;
    font-size: 1.1rem;
    line-height: 1.5;
  }

  .modal-content p strong {
    color: #66bb6a;
  }

  /* Responsive Design */
  @media (max-width: 768px) {
    .modal-content {
      margin: 20px;
      padding: 20px;
      max-width: calc(100% - 40px);
    }
    
    .modal-buttons {
      flex-direction: column;
      align-items: center;
    }
    
    .btn-buy, .btn-confirm, .btn-cancel, .btn-close {
      width: 100%;
      max-width: 200px;
    }
    
    .detail-image, .confirm-image {
      width: 120px;
      height: 120px;
    }
    
    .success-icon {
      width: 60px;
      height: 60px;
      font-size: 30px;
    }
  }
  </style>