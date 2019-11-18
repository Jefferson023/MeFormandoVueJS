<template>
  <div class="animated fadeIn">   
    <b-row>
      <b-col md="12" v-if="comissao">
        <Button @click="criarMensalidade()" type = "button" class="btn btn-primary" style="margin-left:80%;"><i class="icon-plus icons font-2xl"></i> Nova Mensalidade</Button>
      </b-col>
      <b-col lg="12">
        <c-table :table-data="pendentes" :fields="fields" caption = "Pagamentos Pendentes">
          
        </c-table>
      </b-col>

 
    </b-row>
    <b-row>
      <b-col lg="12">
        <c-table :table-data="realizados" :fields="fields2" caption = "Pagamentos Realizados">
          
        </c-table>
      </b-col>
    </b-row>

    
  </div>

</template>

<script>
import axios from 'axios'
import cTable from "./TablePagamento.vue";
export default {
  name: 'pagamentos',
  components: {cTable}, 
  data: () => {
    return {
      pendentes: [],
      realizados: [],
      fields: [
        {key: 'data', label: 'Data', sortable: true},
        {key: 'valor', sortable: true}
      ],
      fields2: [
        {key: 'data', label: 'Data', sortable: true},
        {key: 'valor', sortable: true},
      ],
      comissao: false
    }
  },
  methods: {
    criarMensalidade(){
      this.$router.push("/mensalidade")
    },
  },
  created(){
    axios.get(process.env.VUE_APP_API + "/usuario/confirmadoComissao", {
        headers: {
          "content-type": "application/x-www-form-urlencoded;charset=utf-8",
          token: localStorage.getItem("user_token")
        }
      })
      .then(response => {
        this.comissao = response.data
      })
      .catch(() => {
      });  

    axios.get(process.env.VUE_APP_API + "/pagamento/mensalidades", {
        headers: {
          "content-type": "application/x-www-form-urlencoded;charset=utf-8",
          token: localStorage.getItem("user_token")
        }
      })
      .then(response => {
        var mensalidades = response.data
        mensalidades.forEach(element => {
          if (element.pago == true){
            this.realizados.push([element.mes, element.valor])
          }else{
            var arr = []
            var data = new Date(element.mes)
            arr.push(data.toLocaleDateString())
            arr.push(element.valor)
            this.pendentes.push(arr)
          }
        });
        console.log(response);
      })
      .catch(() => {
      });  
  }  
}
</script>
