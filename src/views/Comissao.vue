<template>
  <div class="animated fadeIn">

    
    
    <b-row>
      <b-col lg="12">
        <c-table :table-data="items" :fields="fields" caption="Comissao" :comissaoPagina="comissaoPagina">
          
        </c-table>
        <!--- Buttão que quero colocar como opção para menbro da (84)99999-9999
       <b-button-group size="sm" class="mx-1">
          <b-btn>New</b-btn>
          <b-btn>Edit</b-btn>
        </b-button-group>
        -->
      </b-col>

 
    </b-row><!--/.row-->

    
  </div>

</template>

<script>
import { shuffleArray } from '@/shared/utils'
import cTable from './Table.vue'

const someData = () => shuffleArray([
  {username: 'Samppa Nori', email: 'teste1@teste.com', telefone: '(84)99999-9999' },
  {username: 'Estavan Lykos', email: 'teste2@teste.com', telefone: '(84)99999-9999'},
  {username: 'Chetan Mohamed', email: 'teste3@teste.com', telefone: '(84)99999-9999'},
  {username: 'Derick Maximinus', email: 'teste4@teste.com', telefone: '(84)99999-9999'},
  {username: 'Friderik Dávid', email: 'teste5@teste.com', telefone: '(84)99999-9999'},

])

export default {
  name: 'turma',
  components: {cTable},
  data: () => {
    return {
      items: someData,
      itemsArray: someData(),
      fields: [
        {key: 'username', label: 'Nome', sortable: true},
        {key: 'email',label:'E-mail'},
        {key: 'telefone'}
      ],
      comissaoPagina:true
      
    }
  }
}
</script>
