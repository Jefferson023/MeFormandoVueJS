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
                        <b-button variant="link" style="margin-left:50%;margin-top:5%" to="/EditarEvento"><i class="icon-note icons font-2xl"></i></b-button>
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
      title: "Titulo",
      price: 1000,
      date:"20/10/2020",
      description:"Lorem ipsum donec accumsan mauris nullam metus aliquam, erat hendrerit pellentesque a purus adipiscing, integer lectus turpis bibendum donec nibh. risus justo eleifend sodales maecenas praesent himenaeos netus magna, metus erat justo vehicula taciti elit taciti potenti scelerisque, conubia diam platea lacus consectetur ac elementum. metus consectetur tristique in elit cursus taciti litora urna, himenaeos ac taciti velit fringilla senectus consectetur elit duis, libero interdum quisque taciti risus eu tortor. cubilia donec diam dapibus volutpat aliquam torquent ultrices, at tortor felis risus id commodo habitant fringilla, diam consectetur vulputate taciti leo imperdiet. ",
      
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
