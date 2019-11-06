<template>
  <div class="animated fadeIn">
  
    <b-row>
      <b-col md="12">
  
        <b-card>
            <div slot="header">
                <b-row>
                <b-col md="11">
                    <h1><strong>{{title}} - {{date}}</strong></h1>
                    </b-col>
                    <b-col md="1">
                        <b-button variant="link" style="margin-left:50%;margin-top:5%" @click="editarEvento()" ><i class="icon-note icons font-2xl"></i></b-button>
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
export default {
  name: 'forms',
  
  data () {
    return {
      selected: [], // Must be an array reference!
      show: true,
      title: "Iria pegar o id : " + this.$route.params.Pid,
      price: "2000",
      date:"2020",
      description:"Texto"
    }
  },
  methods: {
    editarEvento(){
        this.$router.push({name:'Editar Evento',params:{Pid:this.title}})
    },
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
