<template>
  <footer>
    <div class="footer-content">
      <div class="footer-left">
        <p>IF7100 - INGENIERÍA DE SOFTWARE</p>
        <p>Proyecto Uver</p>
      </div>
      <div class="footer-right">
        <p>Luis Alfredo Valverde Torres B98103</p>
        <p>Noelia Maria Alvarado Moreno C00324</p>
        <p>Pablo Cesar Canales Pizarro B91583</p>
      </div>
    </div>
    <p class="copyright">&copy; 2024 Uver. Todos los derechos reservados.</p>
  </footer>
</template>

<script>
export default {
  name: 'FooterComponent',
};
</script>

<style scoped>
footer {
  background-color: #000000;
  color: #fff;
  padding: 1rem;
  text-align: center;
  position: fixed;
  bottom: 0;
  width: 100%;
}

.footer-content {
  display: flex;
  justify-content: space-between;
  margin-bottom: 1rem;
}

.footer-left, .footer-right {
  text-align: left;
  
}

.footer-right {
  text-align: right;
  margin-right: 3%
}
.footer-left {
  text-align: left;
  margin-left: 1.5%
}
.footer-content p {
  margin: 0;
}

.copyright {
  margin-top: 1rem;
  border-top: 1px solid #555;
  padding-top: 0.5rem;
}
</style>
