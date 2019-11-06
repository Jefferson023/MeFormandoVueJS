<template>
  <div class="animated fadeIn">
  
    <b-row v-if="tem_cerimonial">
      <b-col md="12">
  
        <b-card >
            <div slot="header">
                <b-row>
                    <b-col md="11"> 
                        <h1><strong>Cerimonial</strong></h1> 
                    </b-col>
                    <b-col >
                        <b-button type="submit" size="gm" variant="primary" style="margin-left:50%; margin-top:5%" to="/EditarCerimonial"> Editar</b-button>
                    </b-col>
                </b-row>
            </div>
           

                <h3><strong>{{title}}</strong></h3>

            
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

    <b-row v-else>
      <b-col md="12">
  
        <b-card >
            <div slot="header">
                <b-row>
                    <b-col md="11"> 
                        <h1><strong>Cerimonial</strong></h1> 
                    </b-col>
                </b-row>
            </div>
           

                <h3><strong>Não existe um cerimonial cadastrado!!!</strong></h3>
                <b-button type="submit" size="gm" variant="primary" to="/AdicionarCerimonial"> Cadastrar Cerimonial</b-button>

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
      title: "Nome do cerimonial",
      description:"Lorem ipsum donec accumsan mauris nullam metus aliquam, erat hendrerit pellentesque a purus adipiscing, integer lectus turpis bibendum donec nibh. risus justo eleifend sodales maecenas praesent himenaeos netus magna, metus erat justo vehicula taciti elit taciti potenti scelerisque, conubia diam platea lacus consectetur ac elementum. metus consectetur tristique in elit cursus taciti litora urna, himenaeos ac taciti velit fringilla senectus consectetur elit duis, libero interdum quisque taciti risus eu tortor. cubilia donec diam dapibus volutpat aliquam torquent ultrices, at tortor felis risus id commodo habitant fringilla, diam consectetur vulputate taciti leo imperdiet. ",
      price:"1000",
      tem_cerimonial:true
    }
  },
  methods: {
    click () {
      // do nothing
    }
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
