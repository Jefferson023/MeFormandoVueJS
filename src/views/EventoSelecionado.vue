<template>
  <div class="animated fadeIn">
  
    <b-row>
      <b-col md="12">
  
        <b-card>
            <div slot="header">
                <b-row>
                <b-col md="11">
                    <h1><strong>{{title}} - {{date}} {{id}} </strong></h1>
                    </b-col>
                    <b-col md="1">
                        <b-button  v-if="comissao" variant="link" style="margin-left:50%;margin-top:5%" @click="editarEvento()" ><i class="icon-note icons font-2xl"></i></b-button>
                    </b-col>
                </b-row>
            </div>
            <p>
                {{description}}

            </p>

           
            <div slot="footer">
            <b-row>
                <b-col >
                <h2>Preço:R${{price}}</h2>
                
                </b-col>
                
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
      title: "Iria pegar o id : " ,
      price: "2000",
      date:"2020",
      description:"Texto",
      id:this.$route.params.Pid
    }
  },
  
  methods: {
    editarEvento(){
        this.$router.push({name:'Editar Evento',params:{Pid:this.id}})
    },
  },
  created(){
    const data = qs.stringify({id: this.id})
    axios
      .get(process.env.VUE_APP_API + "/evento/eventoSelecionado", {
        headers: {
          "content-type": "application/x-www-form-urlencoded;charset=utf-8",
          token: localStorage.getItem("user_token"),
          id: this.id
        }
        
      })
      .then(response => {
       
       
        if (response.data != null) {
          console.log(response);
          (this.title = response.data[0][0]),
          (this.description = response.data[0][1]),
          (this.date = response.data[0][2]),
          (this.price = response.data[0][3]);
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
