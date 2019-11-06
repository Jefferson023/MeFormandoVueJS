<template>
  <div class="animated fadeIn">
  
    <b-row>
      <b-col md="12">
  
        <b-card>
          <div slot="header">
            <h2><strong>Votação</strong></h2>
          </div>
          <b-form>
            <b-form-group
              label="Pergunta"
              label-for="Pergunta"
              :label-cols="3"
              >
              <b-form-input id="Pergunta" type="text"></b-form-input>
            </b-form-group>
            <b-form-group
              label="Descrição"
              label-for="Descricao"
              :label-cols="3"
              >
              <b-form-input id="Descricao" type="text"></b-form-input>
            </b-form-group>
            <b-form-group
              
              label="Opções"
              label-for="opcao"
              :label-cols="3"
              >
              <b-form-input id="opcao" type="text"></b-form-input>
            </b-form-group>
            <b-button type="submit" size="xm" variant="primary" style="margin-bottom:20px"> Adicionar</b-button>

            <ul v-for="item in items" v-bind:key="item">
                <li :id="'option'+(item.id)">Opção 1 <b-button type="submit" size="sm" variant="danger"> Remover</b-button></li>
            </ul
            >
              


          
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
      show: true,
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
