<template>
  <div class="animated fadeIn">
  
    <b-row>
      <b-col md="12">
  
        <b-card>
            <div slot="header">
                <b-row>
                <b-col md="11">
                    <h1><strong>{{titulo}} </strong></h1>
                </b-col>
                    <b-col md="1">
                        
                    </b-col>
                </b-row>
            </div>
            
            <h4><strong>Data inicial:</strong> {{ dateInicial }}</h4>
            <h4><strong>Data final:</strong> {{ dateFinal }}</h4>
           
            <div slot="footer">
            <b-row>
                <b-col >
                <h2>Custo: R$ {{custo}} - Ganho: R$ {{ganho}}</h2>
                
                </b-col>
                
            </b-row>
            <b-row>
            <div slot="footer">
              <b-button size="xm" variant="primary" @click="editarArrecadacao()">Editar</b-button>
              <b-button size="xm" variant="danger" to="/Arrecadacoes">Voltar</b-button>
            </div>
            </b-row>
              
        </div>
        </b-card>
       
      </b-col>
 
    </b-row>

  

  </div>
</template>

<script>
import axios from 'axios';
import qs from 'qs';
export default {
  name: 'forms',
  
  data () {
    return {
      selected: [], // Must be an array reference!
      show: true,
      titulo: "Iria pegar o id : " ,
      custo: "1000",
      ganho: "2000",
      dateInicial:"2020",
      dateFinal: "2020",
      id:this.$route.params.Pid
    }
  },
  
  methods: {
    editarArrecadacao(){
        this.$router.push({name:'Editar Arrecadacao',params:{Pid:this.id}})
    },
  },
  created(){
    const data = qs.stringify({id: this.id})
    axios
      .get(process.env.VUE_APP_API + "/arrecadacao/projetoArrecadacaoSelecionado", {
        headers: {
          "content-type": "application/x-www-form-urlencoded;charset=utf-8",
          token: localStorage.getItem("user_token"),
          id: this.id
        }
        
      })
      .then(response => {
        if (response.data != null) {
          console.log(response);
          response.data.forEach(element => {          
          (this.titulo = element[0]),
          (this.custo = element[1]),
          (this.ganho = element[2]),
          (this.dateInicial = element[3]),
          (this.dateFinal = element[4]);
          })
        } else {
          alert("Nulo!!!")
        }
      })
      .catch((e) => {
        alert(e)
      });

    axios.get(process.env.VUE_APP_API + "/usuario/confirmadoComissao", {
        headers: {
          "content-type": "application/x-www-form-urlencoded;charset=utf-8",
          token: localStorage.getItem("user_token")
        }
      })
      .then(response => {
        if (response.data == true) {
          this.comissao = true;
        } else {
          this.comissao = false;
        }
      })
      .catch(() => {});
  
  
  
  
  }
}
</script>

<style scoped>
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s;
}
.fade-enter,
.fade-leave-to {
  opacity: 0;
}
</style>
