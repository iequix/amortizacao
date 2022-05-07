<template>
  <div class="container">
    <div class="row">
      <label class="label">Montante : </label>
      <input class="input" type="text" v-model="montante">
      <label class="label">Juros </label>
      <input class="input" type="text" v-model="jurosTotal">
      <label class="label">Parcelas(Mensais)</label>
      <input class="input" type="text" v-model="parcelasTotais">
    </div>
    <button class="button" @click="calc_pagamentos" >
      Calcular
    </button>
    
    <table class="table" cellspacing="10" v-if="pagamentos.length">
      <thead>
        <tr>
          <th>Parcelas</th>
          <th>Pagamento</th>
          <th>Juros</th>
          <th>descontado</th>
          <th>Divida</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="pagamento in pagamentos" :key="pagamento.parcelas">
          <td>{{ pagamento.parcelas }}</td>
          <td>{{ pagamento.pagamento.toFixed(2) }}</td>
          <td>{{ pagamento.juros.toFixed(2) }}</td>
          <td>{{ pagamento.descontado.toFixed(2) }}</td>
          <td>{{ pagamento.divida.toFixed(2) }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  data(){
    return {
      montante: 500000,
      parcelasTotais:0,
      jurosTotal:0,
      pagamentos:[],
    }
  },
  methods:{
    calculo(){
      this.montante = '';
      this.parcelasTotais = '';
      this.jurosTotal = '';
      this.pagamentos=[];
    },
   

    calc_pagamentos(parcelas, divida){
      divida = this.montante
      var parcelas = 0;
      var pagamentos = [];
      let pagamento = 3000;
      do {
        parcelas++
        var juros = 1000
        var descontado = (pagamento - juros)


        divida = divida - descontado

        pagamentos.push({
          divida: divida, pagamento: pagamento,
          juros: juros,
          descontado: descontado,
          parcelas
        });


      } while (divida > 0);
      this.pagamentos = pagamentos;
    }
  }
}
</script>

<style>
.table{
  margin-top: 5%;
  border-top: 1px solid #ccc;
  width: 100%;
}
input {
  max-width: 100px;
  margin-top: 3px;
}
.row {
  display: flex;
  flex-direction: column;
}
.button{
  margin: 6px 0 0 15px;
}
label{
  margin-top: 3px;
}
th{
  text-align: left;
}
</style>
