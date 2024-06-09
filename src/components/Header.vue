<template>
    <header>
      <nav>
        <div class="logo-container">
        <img src="@/assets/img/logouver.jpg" alt="Logo" class="logo"  width="140" height="60">
        </div>
        <ul>
          <li><a href="/">Inicio</a></li>
          <li><a href="/about">Acerca de</a></li>
          <li><a href="/contact">Contacto</a></li>
        </ul>
      </nav>
    </header>
  </template>
  
  <script>
  export default {
    name: 'HeaderComponent',
  };
  </script>
  
  <style scoped>
  
  header {
    background-color: #000000;
    color: #fff;
    padding: 1rem;
  }
  nav {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: auto;
  }
  nav ul {
    list-style: none;
    display: flex;
    gap: 1rem;
    margin-right: 2%;
  }
  nav a {
    color: #fff;
    text-decoration: none;
  }
  .logo-container {
    margin-left: 2%;
  }
  
  </style>
  