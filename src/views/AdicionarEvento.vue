<template>
  <div class="animated fadeIn">
  
    <b-row>
      <b-col md="12">
  
        <b-card>
          <div slot="header">
            <h2><strong>Evento</strong></h2>
          </div>
          <b-form>
            <b-form-group
              label="Titulo"
              label-for="Titulo"
              :label-cols="3"
              >
              <b-form-input id="Titulo" type="text" autocomplete="titulo"></b-form-input>
            </b-form-group>
            <b-form-group
              
              label="Custo"
              label-for="Custo"
              :label-cols="3"
              >
              <b-form-input id="Custo" type="text" autocomplete="custo"></b-form-input>
            </b-form-group>
           
              
            <b-form-group
              label="Data do Evento" 
              label-for="date"
              :label-cols="3"
              >
              <b-form-input type="date" id="date"></b-form-input>
            </b-form-group>
            
            <b-form-group
            
            label="Descrição"
            label-for="basicText"
            :label-cols="3"
            >
            <b-form-input id="basicText" type="text" ></b-form-input>
          </b-form-group>
          
            <div slot="footer">
              <b-button type="submit" size="xm" variant="primary"> Criar</b-button>
              <b-button type="submit" size="xm" variant="danger" to="/Eventos"> Cancelar</b-button>
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
