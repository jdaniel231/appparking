<template>
  
  

  <div id="carro-table">
    <Mensagem :msg="msg" v-show="msg" />
    <div>
      <div id="carro-table-heading">
        <div class="order-id">#</div>
        <div>Nome da Pessao</div>
        <div>Nome da carro</div>
        <div>Placa do carro</div>
        <div>Horario de Entrada</div>
        <div>Ação</div>
      </div>
    </div>

    <div id="carro-table-rows">
      <div class="carro-table-row" v-for='carro in carros' :key=carro.id >
        <div class="order-number">{{ carro.id}}</div>
        <div>{{carro.nome}}</div>
        <div>{{carro.nomeCarro}}</div>
        <div>{{carro.placaCarro}}</div>
        <div>{{carro.hora}}</div>

        <div>
          <select name="status" id="" class="status" @change="updateCarro($event, carro.id)">
            <option value="">Status do carro</option>
            <option :value="statu.tipo" v-for="statu in status" :key='statu.tipo' :selected='carro.status == statu.tipo'>
              {{statu.tipo}}
            </option>
          </select>

          <button class="delete-btn" @click="trash(carro.id)">Excluir</button>
        </div>
      </div>
    </div>

  </div>
</template>

<script>
import Mensagem from './Mensagem.vue';

export default {
  name: "Dashboard",
  data(){
    return{
      carros: null,
      carros_id: null,
      status: [],
      msg: null
    }
  },
  methods: {
    async getCadastro() {
      const req = await fetch('http://localhost:3000/carros');
      const data = await req.json();

      this.carros = data;
      this.getStatus();
    },

     async getStatus() {
      const req = await fetch('http://localhost:3000/status');
      const data = await req.json();
      this.status = data;
    },
    async trash(id){
      const req = await fetch(`http://localhost:3000/carros/${id}`,{
        method: "DELETE",
      });
      const data = await req.json();
      this.msg = `Excluido com sucesso`;
      setTimeout(() => this.msg = "", 3000);
      this.getCadastro();
    },
    
   async updateCarro(event, id){
        const opcoes = event.target.value;
        const dataJson = JSON.stringify({ status: opcoes }); // pega o ID do STATUS e CARROS
        const req =  await fetch(`http://localhost:3000/carros/${id}`, {
            method: "PATCH", // atualiza somente o ID do STATUS
            headers: { "Content-Type" : "application/json" },
            body: dataJson
        });
        const res = await req.json();
          //  Mensagem de cadastro de carro
        this.msg = `Carro do: ${res.nome} foi atualizado para ${res.status} . Obrigado `;
        // Limpar a Mensagem após um tempo
        setTimeout(() => this.msg = "", 3000)
        console.log(res);
        
    }
  },

  mounted(){
    this.getCadastro();
  },
  components: { Mensagem }

}
</script>

<style scoped>
  #carro-table {
        max-width: 1200px;
        margin: 0 auto;
    }
    #carro-table-heading,
    #carro-table-rows
    .carro-table-row {
        display: flex;
        flex-wrap: wrap;
    }
    #carro-table-heading{
        font-weight: bold;
        padding: 12px;
        border-bottom: 3px solid rgba(53,30,180);
    }
    #carro-table-heading div,
    .carro-table-row div {
        width: 19%;
    }
   
   .carro-table-row {
       width: 100%;
       padding: 12px;
       border-bottom: 1px solid rgba(53,30,180);
   }
   #carro-table-heading .order-id,
   .carro-table-row .order-number {
       width: 5%;
   }
    select {
        padding:  10px 6px;
        margin-right:  12px;
    }
    .delete-btn {
        background-color: #3F7FBF;
        color: white;
        font-weight:  bold;
        padding: 10px;
        font-size: 16px;
        border: 2px solid white;
        cursor: pointer;
        transition:  .5s;
    }
    .delete-btn:hover {
        background-color: tomato;
        font-size: 18px;
    }

</style>