<template>
  <Navbar :logo= "logo_src" :alt="app_name" />
  <div class="main-container">
    <router-view/>
  </div>
  <Footer />
</template>

<script>
  import Navbar from  './components/Navbar.vue'
  import Footer from './components/Footer.vue'

  export default {
    components:{
      Navbar,
      Footer
    },
    data() {
      return {
        logo_src:"/img/carro.png",
        app_name:"Cadastre o Carro do Estacionamento"
      }
    }
  }
</script>

<style>
  *{
    margin: 0px;
    padding: 0px;
    box-sizing: border-box;
    font-family: Arial, Helvetica, sans-serif;
  }

  .main-container{
    margin:40px;
    min-height: 250px;
  }

  h1{
    text-align: center;
    font-size: 42px;
    margin-bottom: 40px;
    color: #222;

  }
</style>
