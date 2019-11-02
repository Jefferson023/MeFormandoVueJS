<template>
  <div class="animated fadeIn">

    
    
    <b-row>
      <b-col lg="12">
        <c-table :table-data="items" :fields="fields" caption="<h1>Pagamentos</h1>">
          
        </c-table>
        <!--- Buttão que quero colocar como opção para menbro da comissão
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
import cTable from './TablePagamento.vue'

const someData = () => shuffleArray([
  {mes: 'Janeiro', vencimento: '15/01/2020', valor: '100' ,pago: true},
  {mes: 'Fevereiro', vencimento: '15/02/2020', valor: '100',pago: true},
  {mes: 'Março', vencimento: '15/03/2020', valor: '100',pago: false},
  {mes: 'Abril', vencimento: '15/04/2020', valor: '100',pago: true},
  {mes: 'Maio', vencimento: '15/05/2020', valor: '100',pago: true},

])

export default {
  name: 'pagamentos',
  components: {cTable},
  data: () => {
    return {
      items: someData,
      itemsArray: someData(),
      fields: [
        {key: 'mes', label: 'Mês', sortable: true},
        {key: 'vencimento'},
        {key: 'valor', sortable: true},
        {key: 'pago'},
        

      ],
      
    }
  }
}
</script>
