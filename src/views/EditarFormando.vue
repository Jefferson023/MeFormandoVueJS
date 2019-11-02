<template>
  <div class="animated fadeIn">
  
    <b-row>
      <b-col md="12">
  
        <b-card>
          <div slot="header">
            <h2><strong>Formando</strong></h2>
          </div>
          <b-form>
            <b-form-group
              label="Nome"
              label-for="Nome"
              :label-cols="3"
              >
              <b-form-input id="Nome" type="text" autocomplete="nome"></b-form-input>
            </b-form-group>
            <b-form-group
              
              label="E-mail"
              label-for="Email"
              :label-cols="3"
              >
              <b-form-input id="Email" type="text" autocomplete="custo"></b-form-input>
            </b-form-group>
           
              
            <b-form-group
                label="Cargo"
                :label-cols="3"
                id="basicRadiosCustom"
                value="1"
                stacked>
                <b-row style="margin-left:1%">
                    
                    <div class="custom-control custom-radio"  v-bind:key="item">
                        <input type="radio" id="customRadioFormando"   name="customRadio" class="custom-control-input" value=1>
                        <label class="custom-control-label" for="customRadioFormando" > Formando </label>
                    </div>
                    <div class="custom-control custom-radio"  v-bind:key="item" style="margin-left:1%">
                        <input type="radio" id="customRadioComissao"   name="customRadio" class="custom-control-input" value=1>
                        <label class="custom-control-label" for="customRadioComissao" > Comissão </label>
                    </div>
                </b-row>
                
            </b-form-group>
            

          
            <div slot="footer">
              <b-button type="submit" size="xm" variant="primary"> Salvar</b-button>
              <b-button type="submit" size="xm" variant="danger" to="/Turma"> Cancelar</b-button>
            </div>
          </b-form>
      
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
      show: true
      
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
