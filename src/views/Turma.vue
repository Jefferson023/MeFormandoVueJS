<template>
  <div class="animated fadeIn">

    
    
    <b-row>
      <b-col lg="12">
        <c-table :table-data="items" :fields="fields" caption="TurmaParticipante  ">
          
        </c-table>

      </b-col>

 
    </b-row><!--/.row-->

    
  </div>

</template>

<script>
import { shuffleArray } from '@/shared/utils'
import cTable from './Table.vue'

const someData = () => shuffleArray([
  {username: 'Samppa Nori', email: 'teste@teste.com', cargo: 'Comissão' },
  {username: 'Estavan Lykos', email: 'teste@teste.com', cargo: 'Formando'},
  {username: 'Chetan Mohamed', email: 'teste@teste.com', cargo: 'Comissão'},
  {username: 'Derick Maximinus', email: 'teste@teste.com', cargo: 'Formando'},
  {username: 'Friderik Dávid', email: 'teste@teste.com', cargo: 'Formando'},

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
        {key: 'cargo', sortable: true},
        {key: 'opcoes'}
      ],
      
    }
  }
}
</script>
