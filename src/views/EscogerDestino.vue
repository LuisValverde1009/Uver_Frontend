
<script>
import HeaderComponent from '@/components/Header.vue';
import FooterComponent from '@/components/Footer.vue';

export default {
  name: 'HomeView',
  components: {
    HeaderComponent,
    FooterComponent
  }
};
</script>

<template>
  <div id="home">
    <HeaderComponent />
    <div class="container">

      <div id="escoger-destino">

        <input type="text" placeholder="Buscar destino" class="search-bar" />
        <button class="search-button">Buscar viaje</button>
        
      </div>

    </div>
    <FooterComponent />
  </div>
</template>

<style scoped>
#escoger-destino {
  padding: 20px;
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 10px;
  
}

.search-bar {
  width: 400px;
  padding: 15px;
  font-size: 18px; 
  border: 3px solid #000000;
  border-radius: 4px;
}

.search-button {
  background-color: black;
  color: white;
  padding: 15px 30px; 
  font-size: 18px; 
  border: none;
  border-radius: 15px;
  cursor: pointer;
}

.search-button:hover {
  background-color: #333;
}




</style>

