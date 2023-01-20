<template>
  <div>
    <div id="carro-form">
      <div class="input-container">
        <label for="nome">Nome da pessoa: </label>
        <input type="text" id="nome" v-model="nome" placeholder="Informe o seu nome">
      </div>
      <div class="input-container">
        <label for="nomeCarro">Nome do carro: </label>
        <input type="text" id="nomeCarro" v-model="nomeCarro" placeholder="Informe o seu nome do carro">
      </div>
       <div class="input-container">
        <label for="placaCarro">Placa do carro: </label>
        <input type="text" id="placaCarro" v-model="placaCarro" placeholder="Informe a placa do carro">
      </div>
      <div class="input-container">
        <label for="hora">Horario de entrada: </label>
        <input type="text" id="hora" v-model="hora" placeholder="Informe o horario de entrada: ">
      </div>
      <div class="input-container">
        <input type="submit" class="submit-btn" value="Cadastrar" >
      </div>
    </div>
  </div>
</template>

<script>
export default {
 
}
</script>

<style scoped>
  #carro-form{
    max-width: 300px;
    margin: 0 auto;
  }

  .input-container {
    display: flex;
    flex-direction: column;
    margin-bottom: 20px;
  }
  label {
    font-weight: bold;
    margin-bottom: 15px;
    color: #222;
    padding: 5px 10px;
    border-left: 4px solid #3f7f8f;
  }
  input{
    padding: 5px 10px;
    widows: 300px;
  }

  .submit-btn{
    background-color: #3F7FBF;
    color: white;
    font-weight: bold;
    padding: 10px;
    font-size: 16px;
    border: 2px solid white;
    cursor: pointer;
    transition: .5s
  }

  .submit-btn:hover{
    background-color: green;
    font-size: 18px;
  }
</style>