<template>
  <div class="animated fadeIn">
  
    <b-row>
      <b-col md="12">
  
        <b-card>
            <div slot="header">
                <strong>{{title}}</strong>
            </div>
            <p>
                {{description}}

            </p>
            <b-form>
            
            
                <b-form-radio-group
                id="basicRadiosCustom"
                value="1"
                stacked>
                <div class="custom-control custom-radio" v-for="item in items" v-bind:key="item">
                    <input type="radio" :id="'customRadio'+(item.id)"   name="customRadio" class="custom-control-input" :value=item.id>
                    <label class="custom-control-label" :for="'customRadio'+(item.id)">{{item.option}}</label>
                </div>
                
                </b-form-radio-group>
            
            </b-form>

          <div slot="footer">
              <b-button type="submit" size="gm" variant="primary"> Confirmar</b-button>
              
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
      description:"Lorem ipsum donec accumsan mauris nullam metus aliquam, erat hendrerit pellentesque a purus adipiscing, integer lectus turpis bibendum donec nibh. risus justo eleifend sodales maecenas praesent himenaeos netus magna, metus erat justo vehicula taciti elit taciti potenti scelerisque, conubia diam platea lacus consectetur ac elementum. metus consectetur tristique in elit cursus taciti litora urna, himenaeos ac taciti velit fringilla senectus consectetur elit duis, libero interdum quisque taciti risus eu tortor. cubilia donec diam dapibus volutpat aliquam torquent ultrices, at tortor felis risus id commodo habitant fringilla, diam consectetur vulputate taciti leo imperdiet. ",
      items : [{option:"teste1",id:1},{option:"teste2",id:2},{option:"teste3",id:3}]
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
