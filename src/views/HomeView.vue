


<script>
import HeaderComponent from '@/components/Header.vue';
import FooterComponent from '@/components/Footer.vue';

export default {
  name: 'HomeView',
  components: {
    HeaderComponent,
    FooterComponent
  },
  methods: {
    goToEscogerDestino() {
      this.$router.push({ name: 'EscogerDestino' });
    },
    showNotRequiredMessage() {
      alert('Módulo no requerido');
    }
  }
   
  
};



</script>

<template>
    <div id="home">
      <HeaderComponent />
      <div class="container">
        <div class="section">
          <img src="@/assets/img/cliente.png" alt="cliente" class="section-image">
          <button class="section-button" @click="goToEscogerDestino">Buscar Viaje</button>
        </div>
        <div class="section">
        <img src="@/assets/img/chofer.png" alt="chofer" class="section-image">
        <button class="section-button" @click="showNotRequiredMessage">Empezar a Conducir</button>
      </div>
      </div>
      <FooterComponent />
    </div>
  </template>


<style>
* {
  margin: 0;
  padding: 0;
}

#home {
  display: flex;
  flex-direction: column;
  height: 100vh;
}

.container {
  display: flex;
  flex: 1;
}

.section {
  flex: 1;
  display: flex;
  flex-direction: column;
  align-items: center;
  border: 20px solid #000;
}

.section-image {
  max-width: 100%;
  height: auto;
  margin-bottom: 1rem;
}

.section-button {
  background-color: #000;
  color: #fff;
  border: none;
  padding: 1rem 2rem;
  cursor: pointer;
  font-size: 1.8rem;
  font-weight: bold;
  transition: background-color 0.3s;
  border-radius: 15px;
}

.section-button:hover {
  background-color: #333;
}
</style>
